#### 단위테스트 생성 에러 시 조치요령

1. Test 폴더 생성

   https://ildann.tistory.com/5

2. build.gradle 추가

   https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-api/5.6.0

   ```
   dependencies {
       testCompile group: 'org.junit.jupiter', name: 'junit-jupiter-api', version: '5.6.0'
   }
   ```

3. JUnit5 classpath 생성

   https://stackoverflow.com/questions/42721368/including-junit-5-dependency-in-intellij-idea

4. Intellij Test 실패 발생시 No tests found for given includes

   https://stackoverflow.com/questions/55405441/intelij-2019-1-update-breaks-junit-tests

