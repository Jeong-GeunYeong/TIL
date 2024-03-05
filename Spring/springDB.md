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