### 오늘의 삽질

1. 이슈

   - ajax로 jquery 날리고 json 데이터를 콘솔화면에서 찍어 확인하는데, 데이터 값이 안보이고 Object로만 표시되어 제대로 못받아오는 것인지 혼란스러웠다.
   - QueryString은 정상적으로 확인되었다.

   ![스크린샷 2020-03-12 오후 2 02 04](https://user-images.githubusercontent.com/58318041/76488896-35ca9000-646a-11ea-890a-9d5f0755d992.png)

   ```javascript
   function updateAnswer(e) {
       e.preventDefault();
       var queryString = $(".form-control").serialize();
       var updateBtn = $(this);
       var url = updateBtn.attr("action");
       console.log("url : " + url);
       console.log("queryString : " +queryString);
   
       $.ajax({
           type : 'put',
           url : url,
           data : queryString,
           dateType : 'json',
           error : onError,
           success : updateTemplate
       });
   }
   ```

   ```javascript
   function updateTemplate(data, status) {
       console.log("> " + status);
       console.log("data : " + data);
   }
   ```

2. 솔루션

   - "Data : " string 문자열 제거 후 정상동작 확인하였다.

     ![스크린샷 2020-03-12 오후 2 02 24](https://user-images.githubusercontent.com/58318041/76488931-4f6bd780-646a-11ea-8caa-967e2de8f46b.png)

   ```java
   function updateTemplate(data, status) {
       console.log("> " + status);
       console.log(data);
   }
   ```
