### 오늘의 삽질

1. 이슈

   - 댓글 추가 기능 구현 에서 @OneToMany 맵핑 후 DB에는 입력되지만 실제 화면에서는 댓글이 표시가 안됨

   ```java
   @Entity
   public class Question {
       @Id
       @GeneratedValue(strategy = GenerationType.IDENTITY)
       private Long id;
   
       @ManyToOne
       @JoinColumn(foreignKey = @ForeignKey(name = "fk_question_writer"))
       private User writer;
   
       @NotEmpty
       private String title;
   
       @NotEmpty
       private String contents;
   
       @OneToMany(mappedBy = "question")
       @OrderBy("id ASC")
       private List<Answer> answers;
     	... 생략
   }
   ```

   ```html
   {{#answers}}
   <article class="article" id="answer-1405">
       <div class="article-header">
           <div class="article-header-thumb">
               <img src="https://graph.facebook.com/v2.3/1324855987/picture" class="article-author-thumb" alt="">
           </div>
           <div class="article-header-text">
               <a href="/users/{{writer.id}}" class="article-author-name">{{writer.name}}</a>
               <a href="#" class="article-header-time" title="퍼머링크">
                   {{postingTime}}
               </a>
           </div>
       </div>
       <div class="article-doc comment-doc">
           <p>{{contents}}</p>
       </div>
       <div class="article-util">
           <ul class="article-util-list">
               <li>
                   <a class="link-modify-article" href="/questions/{{question.id}}/answers/{{id}}/form">수정</a>
               </li>
               <li>
                   <form class="delete-answer-form" action="/questions/{{question.id}}/answers/{{id}}" method="POST">
                       <input type="hidden" name="_method" value="DELETE">
                       <button type="submit" class="delete-answer-button">삭제</button>
                   </form>
               </li>
           </ul>
       </div>
   </article>
   {{/answers}}
   ```

2. 솔루션

   - html 파일에서 반복에 필요한 answers에 접근을 못해 화면에 출력이 안됨
   - {{#answer}} -> {{#question.answers}}로 접근 경로 맵핑시켜줌
   - Question class의 answers로 접근하겠다는 의미

   ```html
   {{#question.answers}}
   <article class="article" id="answer-1405">
       <div class="article-header">
           <div class="article-header-thumb">
               <img src="https://graph.facebook.com/v2.3/1324855987/picture" class="article-author-thumb" alt="">
           </div>
           <div class="article-header-text">
               <a href="/users/{{writer.id}}" class="article-author-name">{{writer.name}}</a>
               <a href="#" class="article-header-time" title="퍼머링크">
                   {{postingTime}}
               </a>
           </div>
       </div>
       <div class="article-doc comment-doc">
           <p>{{contents}}</p>
       </div>
       <div class="article-util">
           <ul class="article-util-list">
               <li>
                   <a class="link-modify-article" href="/questions/{{question.id}}/answers/{{id}}/form">수정</a>
               </li>
               <li>
                   <form class="delete-answer-form" action="/questions/{{question.id}}/answers/{{id}}" method="POST">
                       <input type="hidden" name="_method" value="DELETE">
                       <button type="submit" class="delete-answer-button">삭제</button>
                   </form>
               </li>
           </ul>
       </div>
   </article>
   {{/question.answers}}
   ```

   
