# 자주 쓰는 명령어

## Telnet
### Header 조회
```
$ telnet www.naver.com 80
$ GET / HTTP/1.1
$ POST / HTTP/1.1
```

## Bash
### alias
```
$ touch .bash_aliases
$ vi .bash_aliases

alias corelog="tail -f /resource/log/application/out.log"

$ vi .bashrc

# User specific aliases and functions
if [ -f ~/.bash_aliases ]; then
        . ~/.bash_aliases
fi

source .bash_aliases
```