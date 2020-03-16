### 오늘의 강의

### 팀 프로젝트 준비

- 커뮤니케이션 많이하며 팀 프로젝트 연습하기
- 짧은 시간동안 낯선 팀원들과 다양한 프로젝트를 어떻게 풀어갔는지
- 단계적으로 테스트하며 (스프린트) 진행해 나가기
- sprint backlog : 이번주에 해야 할 일 작성 후 시작
- 데일리 스크럼은 필수 (진행상황, 상태 등 파악, 지속적인 개선이 필요)
- github issue 기능 활용하기

### Git을 이용한 Workflow 관리

- commit은 tree, blob 객체로 구성되어 있고, 이 tree는 폴더 구조에 해당한다.

- Git flow에는 여러 방식이 있으니, 하나 선택해서 사용하면 된다.

- 방법1. https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html

  1. git branch feature/login -> prefix를 붙이면 나중에 feature만 볼 수 있다.

  2. 이러한 네이밍 규칙은 팀에서 정한다.

  3. git flow는 merge에 기반한 관리 방식이다.

  4. 완성본에는 tag를 붙이는게 좋다.

  5. master에서는 항상 정상동작하는 소스만 있어야 한다.

- 방법2. http://woowabros.github.io/experience/2017/10/30/baemin-mobile-git-branch-strategy.html

- 방법3. Github workflow (간단함)

- 방법4. Gitlab workflow

- 마스터 브랜치는 깨지말고, 팀워크가 우선이다.
