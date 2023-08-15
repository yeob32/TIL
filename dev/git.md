# Git

## git 파일 생존 주기
![lifecycle](http://git-scm.com/figures/18333fig0201-tn.png)

- 파일은 크게 untracked, unmodified, modified, staged 영역을 거친다.
- untracked : 파일이 있으나 한번도 add 되지 않음.
- unmodified : 파일을 add 하여 commit 을 1회 이상 한 이후, 수정사항 없음
- modified : 바로 위 케이스에서 수정사항 있음
- staged : git add 한 상태

### pull / fetch
- pull : 원격저장소의 내용을 가져와 로컬저장소의 내용과 자동으로 병합작업 수행
- fetch : 원격저장소의 내용을 확인만 하고 로컬저장소의 내용과 병합작업 수행 x
    - $ git fetch <remote>

## Merge

### Merge vs Rebase
- Merge
    - 브랜치 통합
- Rebase
    - 특정 위치로 base 를 옮기고 기존의 commit 재정렬
    - Git History 깔끔해짐
    - master 에서의 rebase 는 피하자

### Squash and Merge
```
$ git checkout devlop
$ git merge --squash iss-1
$ git commit -m "commit-message"
```

### Rebase and Merge
```
$ git rebase -i origin/master
```

### Rebase 주의할 점
- 이미 공개 저장소에 Push 한 커밋을 Rebase 하지 마라
> 이 지침만 지키면 Rebase를 하는 데 문제 될 게 없다. 하지만, 이 주의사항을 지키지 않으면 사람들에게 욕을 먹을 것이다.
- Rebase는 기존의 커밋을 그대로 사용하는 것이 아니라 내용은 같지만 다른 커밋을 새로 만든다. 새 커밋을 서버에 Push 하고 동료 중 누군가가 그 커밋을 Pull 해서 작업을 한다고 하자. 그런데 그 커밋을 git rebase 로 바꿔서 Push 해버리면 동료가 다시 Push 했을 때 동료는 다시 Merge 해야 한다. 그리고 동료가 다시 Merge 한 내용을 Pull 하면 내 코드는 정말 엉망이 된다.

## Git Flow 전략에서의 Merge
- develop - feature 브렌치간 머지
    - Squash and Merge 가 유용하다.
    - feature 의 복잡하고 지저분한 커밋 히스토리를 모두 묶어 완전 새로운 커밋으로 develop 브렌치에 추가하여, develop 브렌치에서 독자적으로 관리할 수 있기 때문
    - 일반적으로 머지 후에 feature 브렌치를 삭제해버리는 점을 떠올려 보면, feature 브렌치의 커밋 히스토리를 모두 develop 브렌치에 직접 연관 지어 남길 필요가 없다.
- master - develop 브렌치간 머지
    - Rebase and Merge가 유용합니다.
    - develop의 내용을 master에 추가할 때에는 별도의 새로운 커밋을 생성할 이유가 없기 때문
- hotfix - develop, hotfix - master 브렌치간 머지
    - Merge 또는 Squash and Merge 모두 유용합니다.
    - 때에 따라 골라 사용하면 좋을 것 같다.
    - hotfix 브렌치 작업의 각 커밋 히스토리가 모두 남아야 하는 경우 Merge, 필요 없는 경우 Squash and Merge 를 사용하면 된다.

## References
- https://code.tutsplus.com/tutorials/rewriting-history-with-git-rebase--cms-23191
- https://meetup.toast.com/posts/122
- https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-Rebase-%ED%95%98%EA%B8%B0