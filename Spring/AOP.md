## AOP가 필요한 상황

- 모든 메소드의 호출 시간을 측정하고 싶다면?
- 공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern)
- 회원 가입 시간, 회원 조회 시간을 측정하고 싶다면?

![AOP](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/AOP1.png "AOP")
-문제-

- 회원가입, 회원 조회에 시간을 측정하는 기능흔 핵심 관심 사항이 아니다.
- 시간을 측정하는 로직은 공통 관심 사항이다.
- 시간을 측정하는 로직과 핵심 비즈니스의 로직이 섞여서 유지보수가 어렵다.
- 시간을 측정하는 로직을 별도의 공통 로직으로 만들기 매우 어렵다.
- 시간을 측저아는 로직을 변경할 때 모든 로직을 찾아가면서 변경해야 한다.

## AOP 적용

- AOP: Aspect Oriented Programming
- 공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern)분리

![AOP2](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/AOP2.png "AOP2")
-해결-

- 회원가입, 회원 조회등 핵심 관심사항과 시간을 측정하는 공통 관심 사항을 분리한다.
- 시간을 측정하는 로직을 별도의 공통 로직으로 만들었다.
- 핵심 관심 사항을 깔끔하게 유지할 수 있다.
- 변경이 필요하면 이 로직만 변경하면 된다.
- 원하는 적용 대상을 선택할 수 있다.

![AOP적용 전 의존 관계](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/AOP3.png "AOP적용 전 의존 관계")

![AOP적용 후 의존 관계](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/AOP4.png "AOP적용 후 의존 관계")

![AOP적용 전 전체 그림](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/AOP5.png "AOP적용 전 전체 그림")

![AOP적용 후 전체 그림](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/AOP6.png "AOP적용 후 전체 그림")