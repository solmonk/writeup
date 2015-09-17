# Hacking

security measure vs attack technique

## CTF

* capture the flag의 약자. 문제를 푼다.
* 크~게 web / forensic / pwnable / reversing / crypto / misc 로 나뉠 수 있다.
* 필드에서 써먹을 것이라는 기대는 하지 않는 것이 좋다.
* 대체로 개발을 잘하는 사람이 해킹도 잘하고 다 잘하는 것 같다. (lokihardt, geohot)
* 그러니까 이 글을 읽는 사람들도 잘 할 것.

## web

* 상당히 실용적이지만 어째 많이 다루어지지 않는다

### sql injection

```sql
select id, pw from users where id='admin' and pw='asdf'
```

* 우려먹어 식상한 고전
* 최근에는 퍼즐급으로 진화함
* 잘하면 sql력이 올라..가나?
* 해킹의 기본 원리를 충실히 따른다.

### XSS

* 고전2이지만 CTF에서는 많이 다루어지지 않아서 (왜일까) 최근 핫함
* 역시 해킹의 기본 원리에 충실하다.

### logical flaw

웹을 가장한 pwnable이라고 생각하면 좋다. 게임에도 들어오는 그런 종류의 공격들. 음수를 넣는다던가.

### php

이 위대한 쓰레기는 해킹당하기 최적화되어 있습니다.

* serialize
* mystery of ==
* strcmp
* echo
* system/exec
* misc

## forensic

툴이 반은 한다. 윈도우용이 많아 좀 슬프다.

### network

* 이건 배워두면 꽤 실용적이다.
* wireshark를 잘 다룰 줄 아는 것이 좋다.

### disk image analysis

* 자살행

### steganography

* 자살행


## crypto

고전암호를 알면 절반은 한다.

### classic

* Caesar
* Substitution
* Vigenere
* 기타 미궁에서나 쓸법한 부호들

### modern

* PKI
* hash collision
* 기타 무서운 것들
* 수학

## misc

* recon
* etc
