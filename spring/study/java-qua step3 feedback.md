### 링크
https://github.com/code-squad/java-qna/pull/168

### step3 피드백

   1. 일반적으로 **필드의 getter는 필드 class 그대로 반환하는 것이 컨벤션**이다. 원하는 포맷으로 반환하고자 한다면 새로 메서드를 추가하는 것이 바람직 하다.

   2. **유틸성 메서드의 경우 static import**하여 사용하면 코드 가독성을 높일 수 있다. (HttpSessionUtils.isLogin -> isLogin)

   3. **Optional을 사용**하여 저장소의 해당 값 null 검사와 조회를 동시에 처리할 수 있다. (findById.get -> findById.orElseThrow)

   4. NullPointerException 같은 경우는 버그로 인식되는 것이기에, try-catch로 정상 플로우를 타게하는 것이아니고 **해당 부분의 null 처리를 진행하고 필요하다면 다른 예외를 발생시켜 처리**하도록 한다. (Optional 처리와 일맥상통)

   5. 예외처리 관련 참고 블로그

      ```
      https://cheese10yun.github.io/spring-guide-exception/
      ```

   6. 객체가 **양방향 연관관계에서 toString Override 시 stackOverflow 이슈 주의**해야 한다. toStringBuilder 클래스 등으로 해결 할 수 있다.

   7. JpaRepository.delete에서 equals, hashmap 이 없음에도 객체를 인식하고 지우는 원리? 우선 해당 entity 조회 후 결과값을 제거하는 것으로 보이는데 잘모르겠음..

      ```
      https://jojoldu.tistory.com/235
      ```
