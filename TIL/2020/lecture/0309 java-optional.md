### 오늘의 강의

### HTTP 웹 서버 구현

- post는 request body를 통해서 내용을 가져온다.
- RequestParameter와 RequestBody는 구분되어 사용해야하지만, 스프링에서는 알아서 해준다.

### Optional

- 객체에서의 null은 비어있음을 의미
- DB에서의 null은 값이 정해지지 않았거나 모름을 의미
- Exception 처리는 try-catch와 throw 두가지로 처리가능
- 객체가 null 일 때 객체의 메서드를 호출하면 NullPointerException 발생됨
- optional은 이런 의도치않은 상황(객체가 null로 리턴되거나, 객체가 null이 될 수 있는)을 방어하기 위해 사용 
- orElse, orElseThrow 등 제공되는 다양한 메서드를 사용할 수 있음
