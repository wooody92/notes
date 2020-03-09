### git 기본명령어

- step1 branch 삭제 : git push origin --delete step1
- local branch 생성 : git checkout -b step1
- 필요한 branch clone : git clone -b step1 https://github.com/wooody92/java-monster-race.git
- commit 되돌리기 : git reset HEAD~
- 브랜치1과 브랜치2 merge : git merge branch2 (현재 branch1을 가리키고 있음) 
- git rebase branch1 :  branch1을 base로 지정하여 현재 branch2를 연결
- 현재작업 임시저장 : git stash
- 임시저장소 삭제 : git stash drop
- 현재 Head 위치로 branch를 가져옴 : git branch -f branch(가져올 브랜치)
- upstream의 해당 브랜치만 추가 : git remote add -t <본인id> upstream
- git 저장소 특정 브랜치만 불러오기 : git clone -b {branch_name} --single-branch {저장소 URL}

-------
### 기초개념

- Add: commit 하기 위한 파일들을 워크스테이션으로 올림
- Fetch: remote repo -> local 가져옴
- Merge: 병합
- Pull = fetch + merge (remote repo -> local 가져와 병합)
- Fork: origin 내 계정 remote repo로 가져옴
- Clon: 내 remote repo에 파일 local로 가져옴
- Push: local 파일 remote로 보냄
- Rebase: Head 브랜치의 베이스를 옮김
- upstream은 commit 가져올수있는 권한만 있음
