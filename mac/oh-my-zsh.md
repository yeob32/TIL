# Oh my ZSH

## Install

### brew
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### zsh
```
$ brew install zsh
```

### Oh my ZSH
```
$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

### Themes
- https://github.com/ohmyzsh/ohmyzsh/wiki/Themes

```
$ vi ~/.zshrc

ZSH_THEME=robbyrussell

$ source ~/.zshrc
```

## Plugin
```
# 기본으로 표시되는 sykim-MacBook-Pro 부분 삭제
$ vi ~/.zshrc

prompt_context() { 
    if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then 
        prompt_segment black default "%(!.%{%F{yellow}%}.)$USER" 
    fi
}

$ source ~/.zshrc
```

### autosuggestions
```
$ brew install zsh-autosuggestions
$ echo "source /usr/local/share/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc # autosuggestions 설치 후 설정
$ source ~/.zshrc # 설정 적용

m1
$ echo "source /opt/homebrew/share/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
```

### syntax highlighter 
```
$ cd ~/.oh-my-zsh/custom/plugins # 디렉토리 이동
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
echo "source ${(q-)PWD}/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc # syntax highlighter 설치 후 설정
$ source ~/.zshrc
```
