### 오늘의 삽질

1. 이슈

   - url을 읽어오는데 {id} 값을 못읽고 null로 읽어와 에러발생

```java
@GetMapping("/questions/{questionId}/answers/{id}/form")
    public String deleteAnswer(@PathVariable Long questionId, Long id, HttpSession session) {
        try {
            System.out.println("questionId > " + questionId);
            System.out.println("id > " + id);   // id > null
            Answer answer = getVerifiedAnswer(id, questionId,session);
            answerRepository.delete(answer);
            return "redirect:/questions/" + questionId;
        } catch (NullPointerException | IllegalAccessException | EntityNotFoundException e) {
            System.out.println("ERROR CODE > " + e.getMessage());
            return e.getMessage();
        }
    }
```

2. 솔루션

   - 맵핑해오고 싶은 데이터 앞에 @PathVariable 하나 더 추가

   - @PathVariable은 하나당 하나씩 사용해야 함

   ```java
   @GetMapping("/questions/{questionId}/answers/{id}/form")
       public String deleteAnswer(@PathVariable Long questionId, @PathVariable Long id, HttpSession session) {
           try {
               System.out.println("questionId > " + questionId);
               System.out.println("id > " + id);
               Answer answer = getVerifiedAnswer(id, questionId,session);
               answerRepository.delete(answer);
               return "redirect:/questions/" + questionId;
           } catch (NullPointerException | IllegalAccessException | EntityNotFoundException e) {
               System.out.println("ERROR CODE > " + e.getMessage());
               return e.getMessage();
           }
       }
   ```
