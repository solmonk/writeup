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
 - 취약한 부분을 찾음
 - 데이터가 어떻게 흘러가는지 봄
 - security measure를 확인
 - 스크립트 작성
* (일단은 말로 설명해 보자)
* http://websec.wordpress.com

* https://github.com/ctfs/write-ups-2014/tree/master/codegate-preliminary-2014/120
* https://kitctf.de/writeups/gits2015/aart/

### XSS

* 고전2이지만 CTF에서는 많이 다루어지지 않아서 (왜일까) 최근 핫함
* 역시 해킹의 기본 원리에 충실하다.
* https://rzhou.org/~ricky/seccon2014/xss_bonsai/gen2.py
* https://github.com/ctfs/write-ups-2014/blob/a0c08f898261cd1bd2deeaf03df892d7001b594d/csaw-ctf-2014/hashes/README.md
* https://github.com/ctfs/write-ups-2014/blob/a0c08f898261cd1bd2deeaf03df892d7001b594d/plaid-ctf-2014/bronies/README.md (csrf+memcorruption+xss)

### logical flaw

웹 어플리케이션을 exploit해 보자. 게임에도 들어오는 그런 종류의 공격들. 음수를 넣는다던가.

* shell command injection
* 기타 온갖 종류의 injection
* https://systemoverlord.com/blog/2014/04/14/plaidctf-2014-reekeeeee/

### php

이 위대한 쓰레기는 해킹당하기 최적화되어 있습니다.

* serialize
* mystery of ==
* strcmp
* echo
* system/exec
* file inclusion
* misc

## forensic

툴이 반은 한다. 윈도우용이 많아 좀 슬프다. hex editor is your friend

### network

* 이건 배워두면 꽤 실용적이다.
* wireshark를 잘 다룰 줄 아는 것이 좋다.
* https://github.com/ctfs/write-ups-2014/blob/a0c08f898261cd1bd2deeaf03df892d7001b594d/csaw-ctf-2014/why-not-sftp/README.md
* https://github.com/ctfs/write-ups-2014/tree/a0c08f898261cd1bd2deeaf03df892d7001b594d/csaw-ctf-2014/big-data
* https://github.com/ctfs/write-ups-2015/tree/master/ghost-in-the-shellcode-2015/forensics/cloudfs

### disk image analysis

* 자살행 (사실 제일 실용적이긴 함)
* https://github.com/ctfs/write-ups-2014/tree/master/plaid-ctf-2014/zfs
* https://github.com/ctfs/write-ups-2014/tree/master/csaw-ctf-2014/fluffy-no-more

### steganography

* 자살행


## crypto

고전암호를 알면 절반은 한다.

### classic

* Caesar
* Substitution
* Vigenere
* 기타 미궁에서나 쓸법한 부호들
* https://ucs.fbi.h-da.de/writeup-csaw-psifer-school/

### modern

* PKI
* hash collision
* 기타 무서운 것들
* 수학
* https://github.com/ctfs/write-ups-2014/tree/master/ghost-in-the-shellcode-2014/gitzino

## misc

* recon
* etc

### pwnable

* 리눅스 관련 지식을 요할 때도 있다.
* 파이썬 문제가 나올 때도 있다.

* heartbleed / shellshock
* https://github.com/ctfs/write-ups-2014/tree/a0c08f898261cd1bd2deeaf03df892d7001b594d/csaw-ctf-2014/pybabbies
* https://blog.inexplicity.de/plaidctf-2013-pyjail-writeup-part-i-breaking-the-sandbox.html
* https://fail0verflow.com/blog/2014/plaidctf2014-pwn375-__nightmares__.html

### extra

* 내가? 이걸? 풀수있나? 하는 생각을 버리자
* 해킹은 기술이고 중요한 것은 번뜩이는 아이디어
* 기술은 48시간 안에도 배울 수 있다
