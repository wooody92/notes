### 오늘의 강의

-----

#### Spring

1. redirect와 foward의 차이
   1. Redirect => 서버가 클라이언트에게 이동할 주소를 알려줘서 이동시킴
      1. Return "redirect:/users" + id;
      2. -> HTTP 301 /localhost:8080/users/1
      3. 브라우저가(주체) 다시 GET /localhost:8080/users/s
   2. 일반적 request (일반적 MVC)
      1. Return "/users/list"
      2. model을 view에게 전달해 주고, view -> /users/list.html 이라는 템플릿을 읽어서 model하고 합쳐서 응답을 해줌
   3. Forward => 요청 -> 서블릿 -> 서블릿 -> 응답
      1. 다른 서블릿 호출해야 Foward 라고 할 수 있음
      2. User controller에서 Question controller 호출하는 것
   4. 요청 -> 서블릿(스프링) -> 응답(컨트롤러)
   5. 요청 -> 컨트롤러의 메서드 -> 응답
