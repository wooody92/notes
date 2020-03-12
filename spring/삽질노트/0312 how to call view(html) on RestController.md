### 오늘의 삽질

1. 이슈

   - @Controller -> @RestController 변경 후 html 파일을 어떻게 불러올까?

   ```javascript
   @GetMapping("/{id}/form")
   public String viewUpdateForm(@PathVariable Long id, Model model, HttpSession session) {
     try {
       model.addAttribute("answer", getVerifiedAnswer(id, session));
       return "/qna/updatedAnswerForm";
     } catch (IllegalAccessException | EntityNotFoundException e) {
       log.info("Error Code > {} ", e.toString());
       return e.getMessage();
     }
   }
   ```


2. 솔루션

   - ModelAndView 클래스를 이용하여 해결할 수 있다.

   ```java
   @GetMapping("/{id}/form")
   public ModelAndView viewUpdateForm(@PathVariable Long id, Model model, HttpSession session) {
     try {
       model.addAttribute("answer", getVerifiedAnswer(id, session));
       return new ModelAndView("/qna/updatedAnswerForm");
     } catch (IllegalAccessException | EntityNotFoundException e) {
       log.info("Error Code > {} ", e.toString());
       return new ModelAndView(e.getMessage());
     }
   }
   ```
   
   #### 참고 블로그
   - https://araikuma.tistory.com/14
   - https://wondongho.tistory.com/76
