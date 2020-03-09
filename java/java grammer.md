## 자바 기초 학습하기
#### 1단계: 아는만큼 정리해서 적어보기(완료) -> 2,3단계: 구글 및 보조자료 참고하여 정리하기(진행중..)

### 오전 미션: 학습 정리

```
- 위 주제 각각에 대해 본인이 중요하다고 생각하는 내용을 정리해서 gist로 제출한다.
- 1단계: 참고자료 없이, 코딩 없이 작성한다.
- 2단계: IDE의 도움을 받아 검증하면서 내용을 수정한다.
- 3단계: 인터넷 검색등 보조자료의 도움을 받아 내용을 수정한다.
- gist로 제출할것
```

#### 1. 변수의 스코프 (유효범위)
- 지역변수(local): 클래스 내부에서 일부 메서드(혹은 어떤 기능을 하는 블럭) 내에서만 사용되는 변수. 메서드 사용이 끝나면 메모리 해제
- 멤버변수(global): 클래스변수 + 인스턴스변수
- 클래스변수: static이 붙음(객체 하나, 인스턴스들이 공유가능), 클래스 변수(인스턴스 변수)로 클래스 안에 존재하는 전체 메서드에서 접근 및 변경 가능한 변수
- 인스턴스변수: 
- 클래스에서 선언된 int a와 클래스 내 메서드에서 선언된 int a는 다르다. (메모리 주소가 다르다.)
- 메서드 내에서 전역변수 접근 및 변경: this.전역변수

#### 1.1 static
- static한 메서드는 클래스가 인스턴스화 되지않아도 사용할 수 있음
- static하게 선언된 변수는 값을 저장할 수 있는 공간이 하나만 생성됨. 그러므로, 인스턴스가 여러개 생성되도 static한 변수는 하나임(메모리 할당을 한번만 함), 인스턴스간 변수 공유시 사용할 수 있음
- 잘 사용하면 메모리관점에서 이점, 잘못 사용하면 객체의 독립성을 헤칠 수 있음

#### 2. 접근 한정자
- public: 모든 클래스에서 접근 가능
- protected: 
- default: 
- private: private이 붙은 변수, 메서드(선언 시 사용)는 해당 클래스에서만 접근가능, 다른 클래스에서는 접근불가, 명시해 주는것이 좋음(캡슐화), 필요할때만 개방(public)
 
#### 3. 객체 지향 프로그래밍
- 왜 사용할까? 복잡도가 높은 프로그램을 디자인하기 쉬움, 유지보수가 목적, 가독성이 중요
- 모듈화: 프로그램을 작성할 때 각 기능별로 나누어 설계 ( 클래스> 입력부, 메인 로직부, 출력부 ...)
- 모듈화.장점: 유지보수 쉬움, 분업 가능
- 모듈화.단점: 설계가 오래걸림
- 추상화: 어떤 객체들에서 공통된 부분을 뽑아내는 것
- 추상화.예시: 가솔린차, 디젤차, 전기차 -> 자동차 프레임 구조로 묶을 수 있음
- 추상화.장점: 재사용성, 유지보수 쉬움

#### 4. 클래스와 인스턴스
- 클래스: 어떤 기능을 위한 설계도, 기능을 위한 변수 선언, 로직들이 구현되어 있음 (메모리 할당 x)
- 인스턴스: 설계도를 통해 생성된 객체, 클래스에 선언된 객체 (메모리 할당 o)
- 객체: 인스턴스들을 일컫는 말 (추상적 개념)
- 예시: 자동차 설계도 및 공정(클래스), 자동차(객체), bmw 320d/hyundai avante(인스턴스)

#### 5. 상속
- 코드 재사용성 및 유지보수를 위해 사용되는 기능들을 추상화하여(공통부를 뽑아내어), 선언하고 자식클래스에서 기능 추가 혹은 변경하여 사용
- extends: 자식 클래스에서 메서드를 추가하여, 부모클래스 + 자식클래스 메서드를 사용
- implements: 부모 클래스에서 선언된 메소드를 전부 사용해야 함 (오버라이딩 가능) ?

#### 6. 추상 클래스
- 추상 메서드가 있는 추상 클래스
- 추상 메서드: 선언만되어있는 메서드
- 추상 클래스에서는 추상 메서드때문에 인스턴스를 만들 수 없음
- 클래스를 추상화 한 것 (클래스의 공통된 부분을 추출한 클래스)
- 추상 클래스를 이용한 문법이 상속인가?

#### 7. 인터페이스
- 클래스는 다중상속이 안되지만, 인터페이스를 통해 다중상속을 쓸 수 있음
- 추상 클래스 개념을 이용하여, 공동작업을 진행하는 개발자들을 위한 규약
- 하나의 프로젝트에서 개발자들이 각기 다른 클래스(모듈)을 개발할 때, 인터페이스를 설정하면 클래스A와 클래스B의 메서드, 메서드 이름 등의 충돌을 방지할 수 있다.

#### 8. 메소드 오버로딩과 오버라이딩
- 오버로딩: 자식 클래스에서 새로운 메서드를 생성하여 부모 클래스 메서드 외에 추가 메서드를 사용하는 것
- 오버라이딩: 자식 클래스에서 부모 클래스의 메서드의 내용을 변경하여 사용하는 것

#### 9. 열거형의 사용법
- 변수를 상수처럼 사용하여, 가독성, 유지보수를 높일 수 있음
- discrete 한 값들을 이용할 때 사용
- enum: 사용되는 string 등의 집합소?

#### 10. 예외 처리
- try-catch / throw
- 개발자가 프로그램에서 발생할 수 있는 에러(원하지 않는 값 등)에 대해서 처리하는 기법
- try{발생 할 수 있는 에러} catch{에러 발생 시 수행 할 로직} throw{ ? } finally{에러 발생해도 진행 될 로직}

#### 11. 컬렉션 프레임워크
- 자료구조를 바탕으로 데이터를 효율적으로 관리하기 위한 Java에서 제공하는 프레임워크
- ArrayList: 탐색속도에 강점을 갖고있는 순서가 있는 자료구조 ?
- HashMap<key, value>: key-value로 묶여있는 순서가 없는 모음, key값은 중복될 수 없지만 value는 중복될 수 있음
- Set: map과 유사하지만 순서가 있음 ?

#### 12. 내부 클래스, 중첩 클래스와 람다
- 람다: 함수형 프로그래밍을 기반, 메서드를 변수?처럼 사용할 수 있는 테크닉, 가독성 등에 장점이 있음 ?
- 함수형 프로그래밍: 외부에 영향을 받지않는 독립적인 메서드? (단순히 어떤 값에 대해서든 input -> output 구조)
- 내부 클래스 ?

#### 13. 스트림
- ?

#### 14. Optional
- null의 존재여부를 명시적으로 입력 ?

#### 15. IO 스트림
- ?