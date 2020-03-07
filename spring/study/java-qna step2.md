### 링크
https://github.com/code-squad/java-qna/pull/149

-----

### 0. Heroku 배포

- https://wooody92.herokuapp.com/

### 1. 구현 기능

- H2 데이터 베이스 개발환경 설정
- 기존 구현했던 기능을 데이터 베이스와 연결
- Step1 피드백 리팩토링
  - LocalDateTime class 사용
  - 5XX HTTP status error 처리 (DB에 존재하지 않는 /users/{id} url 입력 시)
- [@RequestMapping](https://github.com/RequestMapping) 추가
- 회원정보 수정 시 @PutMapping 사용

### 2. 궁금한 것

```
@GetMapping("/{id}")
    public String viewProfile(@PathVariable Long id, Model model) {
        if(!(isIdPresent(id))) {
            return "redirect:/users";
        }
        model.addAttribute("user", userRepository.findById(id).get());
        return "/users/profile";
    }
```

- 위 코드 처럼 존재하지 않는 /users/{id}로 url 접근 시, /users 로 redirect 시켜줬는데 적절한 방법일까요?
