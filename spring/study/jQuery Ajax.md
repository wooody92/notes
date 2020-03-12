### jQuery Ajax 통신

-  jQuery를 이용해서 Ajax 통신을 하는 방법은 아래와 같다.

- jQuery는 Ajax와 관련해서 많은 API를 제공하는데, 그 중 가장 중요한 API가 $.ajax이다.

- ```javascript
  $.ajax({
          type : 'post',
    // 데이터를 전송하는 방법을 지정한다. get, post를 사용할 수 있다.
          url : url,
    // url
          data : queryString,
    // 클라이언트(리퀘스트)에서 서버로 준 데이터 (data -> queryString -> contents="타이핑 값")
          dataType : 'json',
    // 서버측에서 전송한 데이터를 어떤 형식의 데이터로 해석할 것인가를 지정한다. 값으로 올 수 있는 것은 xml, json, script, html이다. 형식을 지정하지 않으면 jQuery가 알아서 판단한다.
          error : onError,
          success : createTemplate
    // 성공 혹은 실패했을 때 호출할 콜백함수를 지정한다.
      });
  ```

- ```javascript
  var queryString = $(".answer-write").serialize();
  // answer-write 클래스의 폼 태그에 맞춰 value값들을 형식에 맞추어 text 형식으로 변환해준다.
  ```

### Event Delegation

- 댓글 추가 후 새로고침 없이 수정 및 삭제 기능들이 바로 동작할 수 있도록 한다.

- ```javascript
  $(".answer-write input[type='submit']").on("click", addAnswer);
  $(".qna-comment-slipp-articles").on("click", ".delete-answer-form button[type='submit']", deleteAnswer);
  ```

- jQuery는 이벤트의 위임을 통해 다수의 요소에 공통으로 적용되는 이벤트 핸들러를 공통된 상위 요소에 단 한번의 연결만으로도 동작할 수 있도록 해준다.

- 각 요소에 연결된 이벤트 핸들러는 화면에 현재 존재하는 요소에는 연결되지만, 새롭게 추가되는 요소에는 연결되지 않는다.

#### 참고 블로그

- http://api.jquery.com/category/ajax/
- https://opentutorials.org/course/1375/6851
- https://araikuma.tistory.com/627
