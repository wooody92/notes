### 오늘의 삽질

1. 이슈

   - 클래스 생성자에서 @Autowired 된 인자를 가져오려하자 NullPointerException 발생했다.

   ```java
   @Component
   public class PageUtils {
       private static final int INITIAL_PAGE_NUMBER = 0;
       private static final int QUESTIONS_OF_EACH_PAGE = 1;
       private static final int SIZE_OF_PAGE_BAR = 5;
       private int firstPage;
       private int lastPage;
       private int totalPage;
       private List<Page> pages;
       long tempCount;
   
       @Autowired
       QuestionRepository questionRepository;
     
   	 public PageUtils() {}
       public PageUtils(int firstPage, int lastPage) {
           this.firstPage = firstPage;
           this.lastPage = lastPage;
           this.tempCount = questionRepository.count();
       }
   }
   ```

   ```java
   <Error Message>
   Caused by: org.springframework.beans.BeanInstantiationException: Failed to instantiate [com.codessquad.qna.PageController]:
   Constructor threw exception; nested exception is java.lang.NullPointerException
   ```

2. 솔루션

   - QuestionRepository를 @Autowired 하기전에 PageUtils 생성자를 먼저 수행하게되는데, 그렇기에 questionRepository에는 비어있는 값으로 null이 들어가있다.
   - 생성자 수행 전에 Autowired를 수행할 수는 없는 노릇이고, 차선책으로 다음 두가지 방법을 생각했다.
   - 1. builder pattern 사용
     2. 해당 클래스에서 QuestionRepsitory 제거 후, 인스턴스 사용 시 questionRepository를 매개변수로 전달받아 사용 (좋은 방법인지는 모르겠다.)

   ```java
   public Page createPage(int pageIndex, QuestionRepository questionRepository) {
     PageRequest pageRequest = PageRequest.of(pageIndex, QUESTIONS_OF_EACH_PAGE);
     Page page = questionRepository.findAll(pageRequest);
     return page;
   }
   ```

