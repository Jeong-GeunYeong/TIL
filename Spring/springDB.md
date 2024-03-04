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
