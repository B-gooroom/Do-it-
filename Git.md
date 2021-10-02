
## Git - flow ?

- git flow = 5가지 종류의 브랜치가 존재
- 항상 유지되는 브랜치 : master, develop
    - master : 제품으로 출시 될 수 있는 브랜치 (상용계)
    - develop : 다음 출시 버전을 개발하는 브랜치 (FITT는 default > develop)(개발계)
- 일정기간 유지되는 브랜치 : feature, release, hotfix
    - feature : 기능을 개발하는 브랜치 (admin 등 아예 추가로 개발되는 서비스?)
    - release : 이번 출시 버전을 준비하는 브랜치
    - hotfix : 출시 버전에서 발생한 버그를 수정하는 브랜치
---

### `git rm`
- 파일삭제/ 스테이지에서 해제할 때
```shell

# 파일삭제
git rm README.md

# README.md 파일을 추적되지 않은 상태로 만들기
git rm --cached README.md

```
----
### `git stash`
- 현재 작업중인 변경점을 임시 저장하거나, 불러올 수 있음
- 현재와 다른 branch로 가서 작업전에 사용하면 유용함
```shell

# 현재 변경점 testStash 라는 이름으로 저장하기
git stash save testStash

# stash ahrfhr(stack) 확인하기
git stash list

# testStash stash 불러와 적용하기
git stash apply testStash

# testStash 라는 stash를 불러와 적용하는데, Staged 상태까지 적용하기
git stassh apply testStash --index

# 가장 최근의 stash를 가져와 적용하고 스택에서 삭제하기
git stash pop

# 가장 최근의 stash 제거하기
git stash drop

# testStash라는 stash 제거하기
git stash drop testStash

```
---
### `git push`
- 원격 저장소(remote repositroy)에 코드 변경분을 업로드 
- 내가 아는 그 push
```shell

# 기본 사용법
git push [저장위치?저장소?] [branch]

# 최초 1회 저장소, branch 지정 (이후 생략 가능)
git push -u [저장위치?저장소?]

# 로컬에서 생성한 branch를 push
git push --set-upstream [저장위치?저장소?]

```
---
### `git pull`
- 원격 저장소(remote repository)의 데어터를 가져온 후 로컬 branch에 합치기
```shell

# git fetch --all && git pull
git pull

```
---
### `git branch`
```shell

# 로컬 branch 목록 확인
git branch

# 원격 저장소를 포함한 모든 branch 목록 확인
git branch -a

# test라는 branch 생성하기
git branch test

# test 로컬 branch를 origin이라는 원격 저장소의 test branch에 연결
git branch --set-upstream-to=origin/test test

# git branch 삭제
git branch -d test

# git branch 강제삭제
git branch -D test

```
---
### `git cherry-pick`
- git cherry-pick = git log에서 특정한 commit 하나만 콕 찝어서 현재 HEAD가 가리키는 branch에 추가
    
    → 다른 branch에 있는 commit을 지금 내 branch에 가져와서 commit 할 수 있게 해줌
    
- 어떤 경우에 사용하게 될까?
    - commit을 다른 브랜치에 잘못했는데 이를 늦게 찾은경우
    - 요구사항이 바껴서 필요없는 commit이 생겼을 경우
        - 해당 commit들 빼고 cherry-pick
    - 수정사항이 생겨 두개의 브랜치에 동시에 commit 해야할 경우
        - 어느 한 브랜치에 commit 후 다른 브랜치에서 cherry-pix
    - 코드 의존성 때문에 다른 사람 commit 중 일부를 가져와야 할 경우

---
