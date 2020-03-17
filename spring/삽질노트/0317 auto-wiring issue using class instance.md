### 오늘의 삽질

1. 이슈

   - 동일한 createPages 메서드 호출 시, PageUtils 객체 생성 후 호출하면 에러가 발생했다.

   ```java
   public List<Page> createPages() {
     PageRequest pageRequest;
     for (int i = 0; i < lastPage; i++) {
       pageRequest = PageRequest.of(pageCount, PAGE_SIZE);
       this.pages.add(questionRepository.findAll(pageRequest));
     }
     return pages;
   }
   
   @GetMapping("/test3")
   public Page viewQuestionList3() {
     List<Page> pages = createPages();
     return pages.get(0);
   }
   
   @GetMapping("/test4")
   public Page viewQuestionList4() {
     PageUtils pageUtils = new PageUtils();
     List<Page> pages = pageUtils.createPages();
     return pages.get(0);
   }
   ```

   ![스크린샷 2020-03-16 오후 7 46 05](https://user-images.githubusercontent.com/58318041/76833218-487c0500-686e-11ea-9f1f-862888441137.png)

2. 솔루션

   - 인스턴스로 새로 생성하면 QuestionRepository 값이 null로 들어온다.
   - 새로 생성된 인스턴스에 대해서는 Autowired가 되지 않는다.
   - Bean을 주입하여야 한다.

   ```java
   
   ```

<img width="569" alt="스크린샷 2020-03-17 오후 1 55 40" src="https://user-images.githubusercontent.com/58318041/76833289-647fa680-686e-11ea-8365-5047e9b9187c.png">

