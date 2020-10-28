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
    
    
    
