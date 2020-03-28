### 오늘의 삽질

1. 이슈

   - Spring Data JDBC 환경에서, 클라이언트에서 POST 요청한 body의 데이터가 null로 들어왔다.
   - Request는 정상적으로 요청 확인했다.

   ```java
   @RestController
   public class ApiUserController {
       Logger logger = LoggerFactory.getLogger(UserController.class);
   
       @Autowired
       UserRepository userRepository;
   
       @PostMapping("/validate/userId")
       public ValidationResult isValidUserId(String userId) {
         	logger.info("Request userId : {}", userId)	// null
           if (userRepository.findByUserId(userId) == null) {
               return ValidationResult.ok();
           }
           return ValidationResult.failure();
       }
   }
   ```

2. 솔루션

   - @RequestBody로 바인딩을 진행하자 정상적으로 값을 가져왔다.

   ```java
   @RestController
   public class ApiUserController {
       Logger logger = LoggerFactory.getLogger(UserController.class);
   
       @Autowired
       UserRepository userRepository;
   
       @PostMapping("/validate/userId")
       public ValidationResult isValidUserId(@RequestBody String userId) {
         	logger.info("Request userId : {}", userId)	// userId
           if (userRepository.findByUserId(userId) == null) {
               return ValidationResult.ok();
           }
           return ValidationResult.failure();
       }
   }
   ```

