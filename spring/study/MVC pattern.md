## MVC 패턴

- 사용자가 controller를 조작하면 controller는 model을 통해서 데이터를 가져오고 그 정보를 바탕으로 시각적인 표현을 담당하는 View를 제어해서 사용자에게 전달한다.

<img width="360" alt="스크린샷 2020-03-08 오후 6 33 36" src="https://user-images.githubusercontent.com/58318041/76160207-788b2000-616b-11ea-9795-8f766c2b21b5.png">

<img width="665" alt="스크린샷 2020-03-08 오후 6 31 18" src="https://user-images.githubusercontent.com/58318041/76160216-8f317700-616b-11ea-87af-3a3134a5df0c.png">

### Model

- 애플리케이션의 정보, 데이터를 나타냄
- 데이타베이스, 처음의 정의하는 상수, 초기화값, 변수 등을 뜻함. 또한 이러한 DATA, 정보들의 가공을 책임지는 컴포넌트를 말함
- 일반적으로 모델은 데이터베이스 테이블에 대응

### View 

- 데이타를 기반으로 사용자들이 볼 수 있는 화면
- View는 클라이언트 측 기술인 html/css/javascript들을 모아둔 컨테이너

### Controller

- Model과 View를 연결시켜주는 역할 (데이터와 사용자인터페이스 요소들을 잇는 다리역할)
- 사용자가 접근 한 URL에 따라서 사용자의 요청사항을 파악한 후에 그 요청에 맞는 데이터를 Model에 의뢰하고, 데이터를 View에 반영해서 사용자에게 알려줌

참고 블로그

```
https://m.blog.naver.com/jhc9639/220967034588
```

