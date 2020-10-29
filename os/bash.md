# Bash

## .bashrc, .bash_profile 차이

### Login Shell / Non-Login Shell
- Login Shell
    - 로그인이란 계정과 암호를 입력해서 Shell 을 실행하는 것
    - 따라서 ssh 로 접속하거나 로컬에서 GUI 를 통해 Shell 을 실행하는 것을 말한다.
    - .profile, .bash_profile 해당 파일들은 로그인 시 로드되는 파일 
        - .profile 은 꼭 bash 가 아니더라도 로그인 시 로드
        - .bash_profile 은 bash 로 로그인 할 떄만 실행
- Non-Login Shell
    - 로그인 없이 실행되는 Shell
    - ex ) ssh 로 접속 후 bash 실행 또는 GUI 세션에서 터미널 띄우는 것
    - sudo bash, su
- ! 맥에서는 로그인 여부 관계 없이 모든 터미널 창을 Login Shell 로 실행 (.bash_profile 로드된다.)

### .bashrc / .bash_profile
- .bashrc
    - 이미 로그인 한 상태에서 새 터미널 창을 열 떄마다 실행 (Non-Login Shell)
- .bash_profile
    - 시스템에 로그인할 때마다 실행 (Login Shell)
- .profile
    - 로그인할 때 로드
    - PATH 처럼 로그인할 때 로드해야 하는데 bash 와 관계 없는 것들을 여기에 넣는다.
- ! 만약 맥에서 새 터미널 창을 열 때마다 .bashrc 를 로드하고 싶다면 .bash_profile 에서 .bashrc 를 로드하면 된다.

