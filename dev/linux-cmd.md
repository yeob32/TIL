# 자주 쓰는 명령어

## Bash
### alias
```
$ touch .bash_aliases
$ vi .bash_aliases

alias corelog="tail -f /resource/log/application/out.log"
alias rm="rm -i"

$ vi .bashrc

# User specific aliases and functions
if [ -f ~/.bash_aliases ]; then
        . ~/.bash_aliases
fi

source .bash_aliases
```

### tcpdump
```
$ sudo tcpdump host 127.0.0.1
```

### scp
```
$ scp -P 22 yeob@192.0.0.1:/app/data/data_20200101.tar /Users/data
```

## Telnet
### Header 조회
```
$ telnet www.naver.com 80
$ GET / HTTP/1.1
$ POST / HTTP/1.1
```

## Linux Command
```
// pbcopy & pbpaste
$ pbcopy < ~/.ssh/id_rsa.pub
$ echo "hello" | pbcopy
$ pbpaste
$ pbpaste > hello.txt

// 명령어 사용법 조회
$ man grep 
$ man ab

$ sleep 100

// 환경변수 및 변수 선언
$ env
$ printenv TERM
$ echo $TERM
$ export env_test=123 => printenv env_test
$ var_test=123 => echo $var_test

// 이전 명령어 실행
$ history 10
$ !1660 => ![history number]

$ echo 'Hello, World!' > sample.txt // 기존 파일 덮어씀
$ echo 'Hello, Foo !!' >> sample.txt // 맨 끝에 추가

//명령어 검색 경로 $PATH
$ printenv PATH
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin => 4개의 디렉토리로 구분
=> printenv 실행 시 4개 디렉토리에서 바이너리 찾은 후 실행

$ which printenv 
/usr/bin/printenv
$ which which
/usr/bin/which
$ which cat
/bin/cat

$ unset PATH
$ printenv PATH
bash: printenv: No such file or directory => printenv 실행 안됨.

// process 종료 상태 코드
$ which printenv
$ echo $?
0 => 성공
$ which fqerqrqrqrq
$ echo $?
1 => 실패

// 파이프, 프로세스 출력 결과를 다른 프로세스로 연결
$ env | grep TERM | sort

// 패키지 매니저
$ brew install some => Mac
$ apt install some => Ubuntu
$ yum install some => CentOS, Red Hat, AmazonLinux
```
