## Request 방식

### @RequestBody

- 요청에 필요한 파라미터를 Body에 넣어 POST 요청하는 방식

- URL에 요청 정보가 노출되지 않는다. 

  ```java
  // http://localhost:8080/test1
  // Body: 12345
  @PostMapping("/test1")
  public String test1(@RequestBody String good) {
    logger.info("result : {}", good);
    return good;
  }
  ```

### @RequestParam

- URL 자체에 요청정보를 포함해 GET 쿼리 요청하는 방식

- 요청 URL이 지저분해 보인다.

  ```java
  // http://localhost:8080/test2?good=12345
  @GetMapping("/test2")
  public String test2(@RequestParam String good) {
    logger.info("result : {}", good);
    return good;
  }
  ```

  ```java
  // http://localhost:8080/test2?good=12345&bad=6789
  @GetMapping("/test4")
  public String test4(@RequestParam String good, @RequestParam String bad) {
    logger.info("result : {}, result2 : {}", good, bad);
    return good;
  }
  ```

### @PathVariable

- RequestParam 방식과 유사하게 GET 요청을 하지만 값만 포함하여 전달

- @={},{} 를 사용하여 여러 값을 한번에 받을 수 있다.

- 공백도 양식에 포함되므로 유의한다.

  ```java
  // http://localhost:8080/12345
  @GetMapping("/test3/{good}")
  public String test3(@PathVariable String good) {
    logger.info("result : {}", good);
    return good;
  }
  ```

  ```java
  // http://localhost:8080/@=12345,6789
  @GetMapping("/test4/@={good},{bad}")
  public String test4(@PathVariable String good, @PathVariable String bad) {
    logger.info("result : {}, result2 : {}", good, bad);
    return good;
  }
  ```

  
