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


