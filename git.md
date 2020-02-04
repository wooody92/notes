### git command

- step1 branch 삭제 : git push origin --delete step1
- local branch 생성 : git checkout -b step1
- 필요한 branch clone : git clone -b step1 https://github.com/wooody92/java-monster-race.git
- commit 되돌리기 : git reset HEAD~
- 브랜치1과 브랜치2 merge : git merge branch2 (현재 branch1을 가리키고 있음) 
- git rebase branch1 :  branch1을 base로 지정하여 현재 branch2를 연결
- 현재작업 임시저장 : git stash
- 임시저장소 삭제 : git stash drop

-------
### git link

- PR (pull request) guide
  https://github.com/code-squad/codesquad-docs/blob/master/codereview/README.md

- git playground
  https://learngitbranching.js.org
  
  
-------
### git PR 규칙

- 프로젝트 파일 포함 /  타겟 파일 불포함입니다. PR 보내기 전에 다른 디렉토리에 해당 브랜치를 클론해 와서 빌드 / 실행할 수 있는지 확인해 보세요. 
- PR은 각 스텝 완료 후에 보내세요. 
- 커밋은 원자 단위로 작성하고 커밋 메시지는 제목 한줄 본문 두 줄 이상 작성해 주세요. 자세하게 
- PR 메시지도 최대한 자세하게 작성해 주세요. 필요하다면 질문을 포함하는 것도 좋습니다. 
- 길게 주석처리한 소스가 간혹 보이던데 그냥 제거해 주세요.  
- PR에 대한 처리는 세 가지가 있습니다.
  1. merge: 정상반영. 코멘트를 읽어 보고 다음 단계에 반영합니다.
  2. Chage request: 수정 요청. 현재 브랜치에서 다시 수정합니다.
  3. closed: 미반영. 지적사항을 읽고 다시 PR을 보내야 합니다.
- PR시 compile 결과물, target directory commit 제외
