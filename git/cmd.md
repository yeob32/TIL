# command

## 버전 관리
- 디렉토리 버전 상태 확인
```
$ git status
```

- 버전 관리 시작 (stage area 에 올리기)
```
$ git add 파일명
$ git add -p (하나씩 올리기) 
```

- commit 메세지 수정
```
$ git commit --amend
```

- commit log
```
$ git log
$ git log -p (변경 코드 같이 보기)
$ git log --pretty=oneline (이력 한줄로 보기)
```

- 변경 코드 확인 (스테이지 올라가지 않은 코드, 즉 add 이전)
```
$ git diff
$ git diff 버전1아이디 버전2아이디 (commit log 2개 비교)
```

- 이전 버전으로 되돌아가기 
```
$ git reset --hard 버전아이디 (현재 로그 삭제하고 돌아간다) -- 위험
$ git revert 버전아이디 (새로운 버전을 만들고 돌아간다)
```

- 푸시 되지 않은 커밋 확인
```
$ git log --branches --not --remotes
```

## 브랜치 관리
- 브랜치 확인
```
$ git branch
$ git branch 브랜치명 (브랜치 생성)
$ git branch -d 브랜치명 (브랜치 삭제)
$ git branch -m 이전 브랜치명 새 브랜치명 (브랜치 이름 변경)
```

- 브랜치 이동
```
$ git checkout 브랜치명
$ git checkout -b 브랜치명
```

## 설정
- 유저 관리
```
$ git config --global user.name 유저명
$ git config --global user.email 이메일주소
```

## 병합 시 충돌 코드 해결
- ==== 를 기준으로 위쪽이 원본, 아래는 merge 한 파일의 사항이 표시된다.
```
>>>>>>>>HEAD
 . . . 
============
 . . . 
<<<<<<<<브랜치명
```