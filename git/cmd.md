# command

## 저장소 관리
- 기본 사용법 
```
$ mkdir ~/MyProject                  => 작업 디렉토리 생성
$ cd ~/myproject                     => 디렉토리로 들어가서
$ git init                           => 로컬저장소로 적용
$ git status                         => 로컬저장소 상태 확인
$ git add 파일                         => git 목록에 파일추가
$ git add .                          => git 목록에 디렉토리의 모든 파일추가
$ git commit -m "commit commnet"        => 로컬저장소에 커밋
  
$ git remote add origin https://github.com/username/myproject.git   => 로컬 저장소와 원격 저장소를 연결
$ git remote -v                 => 연결된 원격저장소 확인
$ git push -u origin master    => 원격저장소에 master 라는 branch 를 생성하고 push
```
- 로컬저장소와 원격저장소 연결
```
$ git remote add origin https://github.com/username/myproject.git
$ git remote -v
```

- 원격저장소 저장
```
-- master branch에 push한다.
$ git push origin master

-- fatal: The current branch master has no upstream branch. => 브랜치가 원격저장소에 없을경우 발생
$ git push -u origin master // 원격저장소에 master 라는 branch 를 생성하고 push

-- ! [rejected]        master -> master (fetch first) 이미 변경된 파일이 원격저장소에 있을경우 발생
$ git pull origin master
```

## 버전 관리
- 디렉토리 버전 상태 확인
```
$ git status
$ git status -sb // 축약 + 브랜치

M : 수정된 파일
A : 추가된 파일
AM : 추가 및 수정 파일
MM : Stage단계에서 수정상태인 파일
?? : Untracked 파일
```

- 버전 관리 시작 (stage area 에 올리기)
```
$ git add 파일명
$ git add -p (하나씩 올리기) 
```

- commit
```
$ git commit -m "message"

// 매번 커밋 할때마다 staging area 에 add 해줘야한다.
// tracked 상태인 파일이 자동으로 추가되기를 원한다면 -a를 추가
$ git commit -am "message" or git commit -a -m "message"
```

- commit 메세지 수정
```
$ git commit --amend
```

- commit log
```
$ git log
$ git log -p // 변경 코드 같이 보기
$ git log --pretty=oneline // 이력 한줄로 보기
$ git log --oneline --decorate  // 브랜치가 어떤 커밋을 가리키는지 확인
$ git log --oneline --decorate --graph --all // 브랜치 커밋 히스토리
$ git log --stat // 변경 라인 수도 같이 보여줌
```

- 변경 코드 확인 (스테이지 올라가지 않은 코드, 즉 add 이전)
```
$ git diff
$ git diff 버전1아이디 버전2아이디 (commit log 2개 비교)
$ git diff --staged
$ git diff --stat --cached origin/master // 대기 중인 커밋 목록
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
$ git branch 브랜치명 // 브랜치 생성
$ git branch -d 브랜치명 // 브랜치 삭제
$ git branch -m 이전 브랜치명 새 브랜치명 // 브랜치 이름 변경
$ git branch -v // 마지막 커밋 함께 보기
$ git branch --merged // 병합된 브랜치만 보기
$ git branch --no-merged // 병합된 브랜치만 보기
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
$ git config --list 
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

## 로컬 Git 변경 제거 방법
```
// 스테이지되지 않은 추적 파일만 제거 , 추적 되지 않은 파일은 제거 안됨
$ git checkout .

// 추적 되지 않는 파일만 제거 , 추적 되는 파일은 제거 안됨
$ git clean -f 

// ** 아래 두가지 방법은 조심 **

// 단계별 추적 및 준비되지 않은 추적 파일만 제거 
$ git reset --hard

// 모든 변경 사항 제거
$ git stash -u
```

## Fork 저장소 Origin 저장소로 부터 Merge
```
$ git remote -v # 내 저장소
$ git remote add upstream "original repo url" # origin 저장소 등록
$ git fetch upstream # origin 저장소 코드 가져옴
$ git merge upstream/master # merge
$ git push origin master 
```

### 파일 잘못 커밋한 경우 저장소 파일 삭제
```
1. 만약 .DS_Store 을 잘못하여 커밋한 경우
2. .gitignore 파일에 .DS_Store 를 등록
3. $ git rm -r --cached .

$ git add .
$ git commit -m “fixed untracked files”
```

### Git 저장소 파일 삭제
```
-- 로컬은 안지워지고 깃저장소만 지워짐
$ git rm —cached file1.txt
$ git rm —cached -r .
$ git commit -m “remove file1.txt”
$ git push origin branch_name
```

## 커밋, 푸시 취소
```
$ git log

// HEAD^ => 헤드의 직전 위치를 의미한다. 즉, 현재 브랜치의 마지막 커밋을 뜻한다.

// 커밋 취소
// [방법 1] commit을 취소하고 해당 파일들은 staged 상태로 워킹 디렉터리에 보존
$ git reset --soft HEAD^
// [방법 2] commit을 취소하고 해당 파일들은 unstaged 상태로 워킹 디렉터리에 보존
$ git reset --mixed HEAD^ // 기본 옵션
$ git reset HEAD^ // 위와 동일
$ git reset HEAD~2 // 마지막 2개의 commit을 취소
// [방법 3] commit을 취소하고 해당 파일들은 unstaged 상태로 워킹 디렉터리에서 삭제
$ git reset --hard HEAD^


// 푸시 취소
// 가장 최근의 commit을 취소 (기본 옵션: --mixed)
$ git reset HEAD^
$ git commit -m "Write commit messages"
$ git push origin [branch name] -f


// 이미 푸시 한 커밋 메세지 수정
$ git commit --amend -m "message"
$ git push -f
```

## stash
```
// working directory에 있는 파일의 상태 확인
$ git status

$ git stash // 스택에 새 stash 추가
$ git stash list
$ git stash apply // 스택에서 작업했던거 다시 가져옴
$ git stash apply [stash_name] // 스택에서 작업했던거 다시 가져옴
$ git stash apply --index // staged 상태까지 저장

// stash 제거
$ git stash drop // 가장 최근 stash
$ git stash drop [stash_name]

$ git stash pop // 적용과 동시에 제거 , apply + drop

## summary
$ git stash save # stash 저장. 개별 파일들을 따로 저장은 불가
$ git stash apply # stash 복원. 복원시 저장된 내용이 삭제되지 않는다.
$ git stash push # stash 저장. 개별 파일 저장 가능.
$ git stash pop # stash 복원. 복원시 저장된 내용이 삭제된다.
$ git stash list # stash로 저장된 내용 확인.
$ git stash clear # stash에 저장된 내용 전부 삭제
$ git stash drop # 개별 stash 저장 내용을 삭제
```