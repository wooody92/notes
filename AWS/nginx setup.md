## NginX 설치 및 환경설정

### nginx 설치

- ```
  sudo apt install nginx
  sudo service nginx start
  niginx -v
  ```

### Nginx 스프링부트 프로젝트 연결하기(리버스 프록시)

- 해당 경로로 이동

  ```
  cd /etc/nginx/sites-available
  ```

- default 파일에 설정파일 추가

  server{} 안에 추가한다.

  ```
  sudo vi default
  ```

  ```
  # Add index.php to the list if you are using PHP
  index index.html index.htm index.nginx-debian.html;
  
  server_name _;
  location / {
  # First attempt to serve request as file, then
  # as directory, then fall back to displaying a 404.
  try_files $uri $uri/ =404;
  }
  location /api/ {
  rewrite ^/api(/.*)$ $1 break; # url에서 other 뒤에 있는 URL을 전부 그대로 사용.
  proxy_pass http://localhost:8080;
  }
  ```

- Nginx 재시작

  ```
  sudo service nginx restart
  ```

- index.html 저장경로
- 아래 default 파일에서 root 경로가 어디로 설정되어 있냐에 따라 다르다.

  ```
  cd /etc/nginx/sites-available
  root /var/www/html;
  
  ------
  
  /var/www/html/
  ```

#### 참고 링크

- https://gist.github.com/kses1010/b0cfb22e96130b49ace8ef19582788b0
- https://gist.github.com/ksundong/7a1c78c2ffbf743e851bf8bfb2762e7f#file-readme-md
- https://jojoldu.tistory.com/267?category=635883
