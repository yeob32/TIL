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