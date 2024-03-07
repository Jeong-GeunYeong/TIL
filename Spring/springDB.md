# 스프링 DB 접근 기술

DataSource는 데이터베이스 커넥션을 획득할 때 사용하는 객체다.
스프링 부트는 데이터베이스 커넥션 정보를 바탕으로 DataSource를 생성하고 스프링 빈으로 만들어둔다. 그래서 DI를 받을 수 있다.
![레퍼지토리](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/Re.png "레퍼지토리")
MemberService는 MemberRepository를 의존하고 있음.
MemberRepository는 구현체로 memoryMemberRepository와 JdbcMemberRepository를 가지고 있음.

![스프링DB](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/SpringDB.png "스프링DB")
스프링 컨테이너의 경우 구현체를 JDBCMemberRepository로만 가지고 있음.

- 개방-폐쇄 원칙(OCP, Open-Closed Principle)
    - 확장에는 열려있고, 수정, 변경에는 닫혀있다.
    - 인터페이스 기반의 다형성, 꼭 인터페이스가 아니다 하더라도 객체지향에서
    말하는 그 다형성이라는 개념을 잘 활용하면 기능을 완전히 변경시켜도
    애플리케이션 전체를 수정할 필요가 없다라고 이해하면 됨.
- 스프링의 DI을 사용하면 **기존 코드를 전혀 손대지 않고, 설정만으로 구현 클래스를 변경 할 수 있음.**
- 회원을 등록하고 DB에 결과가 잘 입력되는지 확인하자.
- 데이터를 DB에 저장하므로 스프링 서버를 다시 실행해도 데이터가 안전하게 저장된다.

- @SpringBootTest : 스프링 컨테이너와 테스트를 함께 실행한다.
- @Transactional : 테스트 케이스에 이 애노테이션이 있으면, 테스트 시작 전에 트랜잭션을 시작하고, 테스트 완료후에 항상 롤백한다.
이렇게 하면 DB에 데이터가 남지 않으므로 다음 테스트에 영향을 주지 않음.

### 스프링 JdbcTemplate

- 순수 Jdbc와 동일한 환경설정을 하면 됨.
- 스프링 JdbcTemplate과 MyBatis같은 라이브러리는 JDBC API에서 본 반복 코드를 대부분 제거해준다. 
하지만 SQL은 직접 작성해야 함.
- 생성자가 하나일 경우 @Autowired생략 가능

### JPA

- JPA는 기존의 반복 코드는 물론이고, 기본적인 SQL도 JPA가 직접 만들어서 실행해준다.
- JPA를 사용하면, SQL과 데이터 중심의 설계에서 객체 중심의 설계로 패러다임을 전환할 수 있다.
- JPA를 사용하면 개발 생산성을 크게 높일 수 있음.

`spring-boot-starter-data-jpa` 는 내부에 jdbc관련 라이브러리를 포함함.
따라서 jdbc는 제거해도 된다.

- `show-sql` : JPA가 생성하는 SQL을 출력한다.
- `ddl-auto` : JPA는 테이블을 자동으로 생성하는 기능을 제공하는데 `none` 를 사용하면 해당 기능을 꺼버림.
    - `create` 를 사용하면 엔티티 정보를 바탕으로 테이블도 직접 생성해줌.

### 스프링 데이터 JPA
스프링 부트와 JPA만 사용해도 개발 생산성이 정말 많이 증가하고, 개발해야할 코드도 확연히 줄어듬. 여기에 스프링 데이터 JPA를 사용하면, 기존의 한계를 넘어 마치 마법처럼, 리포지토리에 구현 클래스 없이 인터페이스 만으로 개발을 완료할 가능. 그리고 반복 개발해온 기본 CRUD 기능도 스프링 데이터 JPA가 모두 제공해줌.
지금까지 조금이라도 단순하고 반복이라 생각했던 개발 코드들이 확연하게 줄어듬. 따라서 개발자는 핵심 비즈니스 로직을 개발하는데, 집중할 수 있다.
실무에서 관계형 데이터베이스를 사용한다면 스프링 데이터 JPA는 이제 선택이 아니라 필수.

**주의 : 스프링 데이터 JPA는 JPA를 편리하게 사용하도록 도와주는 기술입니다. 따라서 JPA를 먼저 학습한 후에 스프링 데이터 JPA를 학습해야 합니다.**

- 스프링 데이터 JPA가 `SpringDataJpaMemberRepositor` 를 스프링 빈으로 자동 등록.
![스프링데이터](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/springJPA1.png "스프링데이터")
![스프링데이터JPA](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/springJPA2.png "스프링데이터JPA")
- 스프링 데이터 제공기능
    - 인터페이스를 통한 기본적인 CRUD
    - `findByName()` , `findByEmail()` 처럼 메서드 이름 만으로 조회 기능 제공
    - 페이징 기능 자동 제공
    
    참고: 실무에서는 JPA와 스프링 데이터 JPA를 기본으로 사용하고, 복잡한 동적 쿼리는 Querydsl이라는 라이브러리를 사용하면 된다. Querydsl을 사용하면 쿼리도 자바 코드로 안전하게 작성할 수 있고, 동적 쿼리도 편리하게 작성할 수 있다. 이 조합으로 해결하기 어려운 쿼리는 JPA가 제공하는 네이티브 쿼리를 사용하거나, 앞서 학습한 스프링 JDBCTemplate를 사용하면 된다.