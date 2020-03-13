### PageRequest

1. 기본 문법

   ```java
   PageRequest pageRequest = PageRequest.of(page, size, sort);
   ```

2. 예제 코드

   ```java
   @RestController
   public class PageController {
       @Autowired
       private QuestionRepository questionRepository;
   
       @GetMapping("/test")
       public Page viewQuestionList() {
           int page = 0;
        		// page는 0번부터 시작
           int size = 3;
         	// 한 페이지에 표시할 객체의 수
         
           PageRequest pageRequest = PageRequest.of(page, size);
           return questionRepository.findAll(pageRequest);
       }
   }
   
   // questionRepository의 모든 객체들의 수를 size(3)으로 나눈다.
   // 나눈 몫이 총 페이지 수 이다. (나머지가 있다면 +1)
   // 위 코드의 경우 0번 페이지를 반환한다. (questionId 1, 2, 3)
   // default 순서 정렬 기준은 id값으로 보인다.
   ```

3. 구현 화면
<img width="784" alt="스크린샷 2020-03-13 오후 6 44 46" src="https://user-images.githubusercontent.com/58318041/76609433-bc5e9a80-655a-11ea-994b-14de00aa1894.png">

