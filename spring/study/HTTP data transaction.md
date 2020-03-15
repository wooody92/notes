### HTTP 동작방식

#### 웹 클라이언트에서 요청을 보내고, 웹 서버에서 응답을 받기까지의 과정에 대해 최대한 구체적으로 설명하시오.

1. 클라이언트(브라우저) 에서 URL을 입력하여 서버에 필요한 요청을 보낸다.

2. URL을 바탕으로 DNS 서버에서 호스트 IP를 조회하여 호스트의 IP를 얻는다.

3. 클라이언트는 웹 서버와 TCP 연결을 시도한다.

   - 서버와의 연결을 확인하기 위해 3-way-handshake 방식을 사용한다.
   - SYN -> SYN-ACK -> ACK

4. 클라이언트는 Request Format에 맞춰 서버에게 특정 명령을 전송한다.

   1. CRUD(Create, Read, Update, Delete) -> (POST, GET, PUT, DELETE)

   2. Request Format 예시

      ```
      GET /index.html HTTP/1.1 -> Request line (요청문)
      Host: www.google.com -> Header
      
      Body:								-> GET 요청이므로 body 내용이 없다.
      ```

5. 서버는 클라이언트의 Request line을 분석하여, 해당 요청의 결과가 처리된 결과인 HTTP status code와 함께 해당 데이터 (웹 페이지)를 회신한다.

   1. 여기에서 클라이언트에서 ajax 등으로 요청하면, json응답을 줄 수도 있다. (요청문에 따라 회신하는 데이터 형식이 다를 뿐, 근본적인 서버의 응답 동작원리는 같다는 의미)

   2. Response Format 예시

      ```
      HTTP/1.1 200 OK	-> Status line (상태문)
      Connection: keep-alive	-> Header
      Content-Type: application/json
      Date: Sun, 15 Mar 2020 07:27:59 GMT
      Keep-Alive: timeout=60
      Transfer-Encoding: chunked	-> Header
      
      Body: <HTML>... 혹은 JSON 응답	-> body
      ```

6. 이렇게 HTTP 요청을 보내고 응답하는 과정을 트랜잭션 (Transaction) 이라고 한다. /index.html 웹 페이지를 불러오는 과정에서 html 파일에 특정 이미지를 출력하기 위해 이미지 url이 들어있을 수 있다. 웹 브라우저에서 html 파일을 읽으며 위와 같이 내부에 요청이 필요하다면 내부적으로 해당 url에 요청과정이 반복되며 트랜잭션이 일어난다. (하나의 웹 페이지를 출력하기위해 내부적으로 여러번의 트랜잭션이 일어날 수 있다.)

7. 트랜잭션이 끝나면 서버와 클라이언트는 4-way-handshake로 연결을 종료한다.

   - ```
     Client -> Server : FIN
     Server -> Client : ACK
     SERVER -> Client : FIN
     Client -> Server : ACK
     ```

8. 매번 트랜잭션이 일어나기전에 연결하고 끊는 과정은 자원낭비가 될 수 있다. HTTP/1.1 부터는 지속적인 연결의 경우 자원낭비를 막기위해 keep-alive 헤더가 추가되어 TCP 연결이 지속된 상태로 데이터를 송수신 할 수 있다.
