## 쿠키와 세션

### 왜 사용할까?

- HTTP는 stateless, connectionless한 특성이 있기때문에, 클라이언트가 누구인지 구분하기위해 사용함
- 클라이언트에서 웹페이지를 요청하면 서버에서 쿠키와 함께 응답하고, 그 쿠키는 클라이언트 로컬에 일정 시간 저장되어 페이지 요청시마다 쿠키와 함께 request 한다.

- connectionless

  ```
  HTTP는 먼저 클라이언트가 request를 서버에 보내면, 서버는 클라이언트에게 요청에 맞는 response를 보내고 (일정 시간 후에) 접속을 끊는 특성
  ```

- Stateless 

  ```
  연결을 끊는 순간 클라이언트와 서버의 통신이 끝나며 상태 정보는 유지하지 않는 특성
  예) 쿠키와 세션을 사용하지 않으면 쇼핑몰에서 옷을 구매하려고 로그인을 했음에도, 페이지를 이동할 때 마다 계속 로그인을 해야 함
  ```

### 쿠키

- 쿠키는 클라이언트(브라우저) 로컬에 저장되는 키와 값이 들어있는 작은 데이터 파일

- 쿠키는 클라이언트의 상태 정보를 로컬에 저장했다가 참조

- 쿠키는 사용자가 따로 요청하지 않아도 브라우저가 Request시에 Request Header를 넣어서 자동으로 서버에 전송

- 쿠키의 동작 방식

  ```
  1. 클라이언트가 페이지를 요청
  2. 서버에서 쿠키를 생성
  3. HTTP 헤더에 쿠키를 포함 시켜 응답
  4. 브라우저가 종료되어도 쿠키 만료 기간이 있다면 클라이언트에서 보관하고 있음
  5. 같은 요청을 할 경우 HTTP 헤더에 쿠키를 함께 보냄
  6. 서버에서 쿠키를 읽어 이전 상태 정보를 변경 할 필요가 있을 때 쿠키를 업데이트 하여 변경된 쿠키를 HTTP 헤더에 포함시켜 응답
  ```

- 예) 장바구니, 자동로그인, "오늘 더이상 이 창을 보지않음" 팝업 등

### 세션

- 세션은 쿠키를 기반하고 있지만, 사용자 정보 파일을 브라우저에 저장하는 쿠키와 달리 세션은 서버 측에서 관리

- 서버에서는 클라이언트를 구분하기 위해 세션 ID를 부여하며(서버측에서 생성) 웹 브라우저가 서버에 접속해서 브라우저를 종료할 때까지 인증상태를 유지, 일정 시간 응답이 없다면 인증해제

- 사용자에 대한 정보를 서버에 두기 때문에 쿠키보다 보안에 좋지만, 사용자가 많아질수록 서버 메모리를 많이 차지하게 됨 (동시접속자 많을 시 서버 과부하로 성능 저하의 요인)

- 클라이언트가 Request를 보내면, 해당 서버의 엔진이 클라이언트에게 유일한 ID를 부여하는 데 이것이 세션ID (Hash로 암호화 되어 저장된 값)

- 세션의 동작방식

  ```
  1. 클라이언트가 서버에 접속 시 세션 ID를 발급
  2. 클라이언트는 세션 ID에 대해 쿠키를 사용해서 저장하고 가지고 있음
  3. 클라리언트는 서버에 요청할 때, 이 쿠키의 세션 ID를 서버에 전달해서 사용
  4. 서버는 세션 ID를 전달 받아서 별다른 작업없이 세션 ID로 세션에 있는 클라언트 정보를 가져옴
  5. 클라이언트 정보를 가지고 서버 요청을 처리하여 클라이언트에게 응답
  ```

- 로그인 동작방식

  ```
  1. userID, password(암호화 진행) 후 DB와 일치여부 확인
  2. 일치하는 데이터가 있으면 서버DB의 해당 계정정보 테이블에 sessionID 생성 후 클라이언트에게 응답
  3. sessionID는 보안 상 로그인 할때마다 변경되는 것이 바람직함
  
  https://www.slideshare.net/HeeminKim2/how-loginworks
  ```

### 쿠키와 세션 차이?

- 쿠키와 세션은 비슷한 역할을 하며, 동작원리도 비슷함. 세션도 결국 쿠키를 사용하기 때문

  사용자 정보가 저장되는 위치 (쿠키는 클라이언트, 세션은 서버)

- 세션은 보안에서 강점이있고, 쿠키는 요청속도에서 강점이 있음 (세션은 서버에서 처리하기 때문)

- 서버 과부화를 방지하기위해 쿠키와 세션을 나누어 사용함

참고 블로그

```
https://interconnection.tistory.com/74
https://cjh5414.github.io/cookie-and-session/
```

