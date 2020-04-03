## Front Web Server 배포

### node.js 설치

- npm 명령어를 사용하기 위해 설치한다.

- curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash

  ppa node.js가져오기

- sudo apt-get install -y nodejs

  node.js 설치

- sudo apt-get install build-essential

  npm 제기능 install

### Webpack 묶기 및 Apache 폴더로 옮기기

- 프론트 html 및 js 파일들을 하나의 html, 하나의 js로 엮어주는 작업

- npm install

- npm run build

- sudo cp -a * /var/www/html/

  dist 디렉토리 내 index.html 및 .js 파일 아파치 웹서버 경로로 이동한다.

- 80포트로 접속해보기
