### application-secret.properties 사용하기

- application.properties :  spring.profiles.active=secret 추가

- Application-secret.properties : 데이터 추가 (DATA = test)

  필요한 경우가 아니라면 쌍 따옴표는 꼭 제거하도록 하자 ("String" -> String)

- 아래처럼 사용할 수 있다.

  ```
  @Value("${DATA}")
  private String data;
  ```

- gitignore에 추가하여 비밀키 등을 보호한다. (해당 파일명 작성 및 이전에 올렸었다면 캐시 지워야한다)

- 주의사항 : **배포 할 때는 gitignore 한 해당 properties 파일을 새로 추가해줘야 참조가능해서 에러가 발생하지 않는다.**
