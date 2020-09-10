# Git

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