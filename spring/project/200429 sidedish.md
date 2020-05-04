## SIDEDISH

- https://github.com/codesquad-member-2020/sidedish-11

### TODO

- [x] 테이블 설계
- [x] DTO Wrapper 추가
- [x] MySQL 연결 테스트
- [x] ERD 작성
- [x] 데이터 받아와서 입력하기
- [x] 가격 관련 데이터 Integer 타입 변경
- [x] 각 카테고리 항목 별 데이터 출력해보기
- [x] 디테일 아이템 출력해보기
- [x] JDBC Template 이용 DAO 학습 및 구현
- [x] OAuth 학습 및 구현
- [x] OAuth 로그인 후 리다이렉트
- [x] 주문하기 기능
- [x] 주문 품절 관련 기능
- [x] 사진 url 데이터 추가하기
- [x] 베스트 아이템 기능 시간관계 상 포기
- [x] 색상 추가하기
- [x] tomcat 설치 &  war 배포
- [x] git과 bash, crontab을 이용해서 자동 배포스크립트를 작성

-----

### Study Keyword

- [ ] @Builder
- [ ] Aggregation
- [x] RestTemplate
- [x] HttpEntity
- [ ] @Transactional
- [ ] HttpHeaders
- [x] DTO, DAO
- [x] JDBC Template 
- [ ] JdbcTemplate.query vs. JdbcTemplate queryForObject
- [x] OAuth
- [x] Tomcat



-----

### Daily Log

#### 0420 (월)

- 기획서 분석
- 도메인 분석
- 개발환경 구축

#### 0421 (화)

- DB 설계
- CORS config 설정
- 프로젝트 기본 구조 작성 (Global Exception Handler 등)
- 클래스 구조에 대한 생각
- DAO, DTO 학습
- 생활코딩 MySQL 시청

#### 0422 (수)

- 전체 구조에 대한 생각
- DB 재설계
- DTO 사용 Wrapping
- 프로젝트 일지 작성 (이것)

#### 0423 (목)

- OAuth 학습
- Github - OAuth 클라이언트 등록
- Github - OAuth AccessToken 받기 구현
- Github 로그인 유저 정보 Api 받기 구현
- MySQL 연동 버그 수정 (테이블에 primary_key 하나라도 없으면 에러 발생)

#### 0424 (금)

- 회고
- 기본 mock 데이터 입력
- 아이템 세부사항 (/detail/{hash}) dto 응답
- 카테고리 dto 생성

#### 0425 (토)

- 카테고리 dto에 아이템 리스트도 아이템 dto 타입에 맞게 변경
- 전체 카테고리 dto 응답 api 구현
- 카테고리의 개별 아이템 출력 버그 수정
- API 문서 및 배포일지 작성
- 상품 재고 추가
- 상품 주문 기능 추가
- 재고 품절 시 품절 뱃지 추가 기능 추가
- 뱃지 색상 응답 dto에 추가

#### 0426 (일)

- 클라이언트 요구사항 논의
- 가격 및 포인트 인티저 타입으로 변경
- 상품 디테일 응답값에 타이틀 추가
- DAO 학습
- Item dao 작성 -> 조인을 사용해서 쿼리 수 줄여보기
- 테스트 코드 작성
- Dao 존재하지 않는 데이터 조회 시 예외처리 작성
- Category dao 작성

#### 0427 (월)

- OAuth 로그인 시 메인화면으로 리다이렉션 추가

- OAuth 로그인 및 리다이렉트 방식 고민

  ```
  방법1) 프론트 : github oauth link 연결 -> 백엔드 : 응답값 받아 서버 메인화면으로 redirect => O
  방법2) 프론트 : login api로 fetch 요청 -> 백엔드 : 서버 자체에서 github oauth link로 redirect 후 다음 진행사항은 방법1과 동일 -> 처음에는 github 자체에서 CORS 에러 발생(http, https 차이에서 발생하는 에러) 라고 생각함 -> nginx 80 포트로 오는 요청에서만 에러 발생 => X
  방법3) 백엔드 : NGinx에서 포트 포워딩 => ?
  ```

- 리다이렉트 시켜주면 데이터는 어디에 넣는걸까?

- 상품 2개 이상 주문 시 처리하는 기능 추가

- Api doc 및 배포일지 업데이트

#### 0428 (화)

- 상품 정량 주문 시 품절 뱃지 안생기는 버그 수정
- 상품 초과 주문 시 품절 뱃지 생기는 버그 수정
- 로그인 시 쿠키를 이용하여 사용자 userId 전송
- 상세페이지 사진 url 데이터 추가
- 톰캣 설치 및 war 배포

#### 0429 (수)

- 데모

-----

### 아쉬운 점

- CRUD DAO로 구현 (쿼리 수 줄이기)
- N:M 테이블 구조 설계



### 피드백

- 1주차

<img width="1570" alt="스크린샷 2020-04-29 오후 6 20 35" src="https://user-images.githubusercontent.com/58318041/80580326-549adb00-8a46-11ea-9320-f1216efb1909.png">


-----


### 회고 (Apr 25, 2020)

이번 배민찬 프로젝트는 페어가 없이 혼자 하게 되었다. 스케쥴 관리, 기능 구현에 있어 내가 하고싶은 대로 구현하면 되기 때문에, 강의 있는 날을 제외하고는 학원에 나올 일이 별로 없을거라고 생각했다. (집에서 코드스쿼드까지는 왕복 3시간이기 때문에 이동 시간이 조금 아까웠다.)

프로젝트를 시작하고 집에서 DB 구조에 대해 생각하고, 전체 코드에 대한 구조를 생각했다. 구조가 마음에 들지는 않았지만, 생각도 안나고 설계의 늪에 빠질것 같아 너무 많은 시간을 쏟지 않고 진행하며 바꿔 나가기로 했다. 그래서 처음부터 DB 설계를 탄탄하게 하고 프로젝트를 쭉쭉 진행하는 분들을 보면 대단하다고 생각이 들었다.

하루 집에서 하고, 다시 코드스쿼드에 나갔다. 혼자하면서, 다른 사람들은 어떻게 생각할까 하고 궁금했던 점과 이해가 가지 않았던 부분들에 대해서 백엔드 동기들 여럿에게 생각을 묻고 다녔다. 결과는 기대보다 좋았다. 비슷한 고민을 하던 사람도 있었고, 좋은 의견도 많이 들을 수 있었다. 혼자 집에서 하면 이렇게 생각을 할 수 있었을까? 엄청 많은 시간이 들었겠지 라고 생각이 들었다. 그 뒤로 매일 코드스쿼드에 출근한다. 같이 하는게 재밌기도하고, 혼자 생각에 빠져 허우적거리는 것보다 물어보고 대화하며 하는게 배우는 점이 더욱 많다고 느꼈다.

회원가입부터 미세먼지, TODO 프로젝트를 주욱 진행해오면서, 새로운 용어도 많이 배우고 다양한 기술도 많이 배운거 같다. 그러다 문득 나중에 다시 봤을때 그때 그 프로젝트에서 뭐 공부하고 뭐 배웠었지? 하고 생각할 것 같았다. 실제로 요새도 당장 지난주에 구체적으로 뭐했었는지 잘 기억도 안난다.. 매일 뭔가를 배우기도하고는 핑계고, 사실 프로젝트 하기 바빠서 정리를 잘 안해서 그런 것 같다. 그래서 이번 프로젝트 부터는 기록을 하기로 했다. [프로젝트 기록](https://github.com/wooody92/notes/blob/master/spring/project/200422 sidedish.md) 을 만들었고 나중에 누군가 그 프로젝트 때 뭐했어요? 라고 물어보면 대답 할 수 있도록 그때의 생각들을 적어 놓으려고 한다.

노트에는 미뤄놓은 학습 키워드들이 아직 산더미처럼 쌓여있다. 계속 뭔가 학습해야할게 생겨서 스택처럼 이전에 미뤄두었던 키워드들은 뭔가 쌓여가기만 한다. 그래도 아직은 그냥 이렇게 다른 걱정없이 공부만 하는게 즐겁다. 하지만 어느덧 코드스쿼드 과정도 점점 끝나간다. 다시 취업전선에 뛰어들 생각을 하니, 한번 해봐서 그런가 생각만해도 스트레스가 한가득이다. 취업준비도 알고리즘부터 차근차근 시작해야하는데 매일 이렇게 생각만하고 현실은 프로젝트 마감에 치여 아무것도 하지 못한다. 그래서 과정이 끝나갈수록 점점 걱정도 많아지는 것 같다.

인생 길게보고 초조해하지 않으려고 한다. 잘 다니던 회사를 그만두고, 아직 배우는 과정이지만, 개발자로 업종 전환 한 것만으로도 남은 인생에 있어 큰 가치가 있다고 생각한다. 그러니 지금 주어진 일에 집중하도록 하자.


-----

## 고민사항

### DTO와 OAuth

- DTO의 생성자에서 for문을 돌리는 것은 괜찮은가? -> setter vs. constructor ?
- ERD에는 DTO로 포장된 것도 그려야 할까? -> 테이블 만 저장한다.
- OAuth로 회원가입하면 액세스 구별을 위해 DB에 무슨정보가 저장될까? -> **email과 token(암호화)**

### DB

- 아이템 테이블은 하나로 하고, @Embedded를 이용하여 객체를 분야별로 나눈다. -> DTO 설계로 변경
- 의문점1 : @Embedded 1:1 관계에서 중복되는 부분은 어떻게 처리??  -> 하나 테이블로 통일 후 DTO 설계
- 의문점2 : delivery_type / badge 같이 DB에 배열로 저장할 수 없을까? 방식은?  -> DTO로 한번더 Wrapping
- 의문점3 : 카테고리 - 카드 구조에서 카드 전체 primary id로 접근하는 것과, 카테고리 id - 카드 카테고리 키로 접근하는 것중 뭐가 더 좋을까? -> JDBC에서는 하나의 aggregation root의 하나의 repository로 사용을 권장하기 때문에 후자이겠지만, 나는 전자로 진행했다. 
- 의문점4 : 데이터는 제공된 mockAPI에서 파싱해와야 하는 것 인가? 수동으로 가져와야 하는 것인가? -> RestTemplate 으로 파싱해보자

-----

### PR 및 질문

- https://github.com/codesquad-member-2020/sidedish-11/pull/58

### 학습

- 배민찬 API 기능 구현
- DTO를 사용하여 원하는 JSON 형태로 데이터 가공하기
- Jdbc Template을 사용하여 DAO 생성
- OAuth를 사용한 로그인 기능 구현

### 질문

- 처음 DTO 이용하여 데이터를 가공해보았는데, 아래처럼 리스트 타입으로 데이터를 가공해야 할 때 아래처럼 생성자에서 반복문을 사용하였습니다. 굉장히 어색하게 느껴지지만 별다른 좋은 방법이 생각나지 않는데, 어떤 방식으로 처리해야 좋을까요?

```java
public class ItemResponse {
    @JsonIgnore
    private Long id;
    private String detail_hash;

    @JsonProperty("badge")
    private List<String> badgeStrings = new ArrayList<>();

    public ItemResponse(Item item) {
        this.id = item.getId();
        this.detail_hash = item.getHash();

        for (Badge badge : item.getBadges()) {
            badgeStrings.add(badge.getName());
        }
    }
```

- DAO는 Entity와 DTO 중 어느 곳에 작성되어야 할까요? 저는 Entity에 관하여 DAO를 작성하였고 그 Entity 객체를 활용하여 DTO를 생성했습니다. DTO 클래스를 만들고 필요한 데이터를 DAO를 이용하여 맵핑시키는 게 맞는 방법일까요?

- 제가 작성한 ItemDao 클래스에서 아래와 같이 하나의 아이템을 조회하는데 관계형 테이블로 연결된 항목들을 조회하기위해 여러번 쿼리를 요청합니다. 좋은 방식이 아니라고 생각이 듭니다. JOIN을 이용하면 쿼리 수를 줄일 수 있을까요? 아니면 어떤 방법이 있을까요?

```java
private Item getItem(ResultSet rs, Long id) throws SQLException {
        Item item = new Item();
        item.setId(rs.getLong("id"));
        item.setHash(rs.getString("hash"));
        item.setImage(rs.getString("image"));
        item.setTitle(rs.getString("title"));
  
  			// 여기서 아이템 테이블과 관련된 다른 테이블 조회 요청
        item.setBadges(getBadges(id));
        item.setDeliveryTypes(getDeliveryType(id));
        item.setThumbImages(getThumbImage(id));
        item.setDetailSections(getDetailSection(id));
        item.setColors(getColor(id));
        return item;
    }

private List<Badge> getBadges(Long itemId) {
        String sql = "SELECT badge.id AS id, badge.name AS name, badge.item_key AS item_key" +
                " FROM badge" +
                " WHERE badge.item = ?" +
                " ORDER BY item_key";

        RowMapper<Badge> badgeMapper = (rs, rowNum) -> {
            Badge badge = new Badge(rs.getString("name"));
            badge.setId(rs.getLong("id"));
            return badge;
        };
        return jdbcTemplate.query(sql, new Object[] {itemId}, badgeMapper);
    }
```


