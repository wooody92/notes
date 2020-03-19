### 오늘의 삽질

1. 이슈

   - @Component로 클래스를 bean으로 만든 후, 생성자를 만들때마다 오류가 발생했다.

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
   
       public PageUtils(int firstPage, int lastPage) {
           this.firstPage = firstPage;
           this.lastPage = lastPage;
       }
   }
   ```

   ```java
   <Error Message>
    org.springframework.beans.factory.NoSuchBeanDefinitionException: No qualifying bean of type 'int' available: expected at least 1 bean which qualifies as autowire candidate. Dependency annotations: {}
   
   ```

   <img width="811" alt="스크린샷 2020-03-20 오전 12 14 43" src="https://user-images.githubusercontent.com/58318041/77083040-35b92a00-6a40-11ea-81c6-cbdc399c6b82.png">

   

2. 솔루션

   - Spring Bean에서는 생성자 사용 시, **public PageUtils() {}** 와 같이 비어있는 생성자를 한번 더 선언해줘야 한다.

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
   
       public PageUtils() {}
       
       public PageUtils(int firstPage, int lastPage) {
           this.firstPage = firstPage;
           this.lastPage = lastPage;
       }
   
       public void initPage(QuestionRepository questionRepository) {
           Page page = createPage(INITIAL_PAGE_NUMBER, questionRepository);
           totalPage = page.getTotalPages();
           if (totalPage < SIZE_OF_PAGE_BAR) {
               lastPage = totalPage + 1;
           }
       }
   }
   ```

