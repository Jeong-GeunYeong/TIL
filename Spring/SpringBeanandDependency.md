# 스프링 빈과 의존관계

![container1](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/container1.png "container1")
- 참고: helloController는 스프링이 제공하는 컨트롤러여서 스프링 빈으로 자동 등록된다.  
@Controller가 있는 경우 자동 등록됨
- 스프링 빈을 등록하는 2가지 방법
    - 컴포넌트 스캔과 자동 의존관계 설정
    - 자바 코드로 직접 스프링 빈 등록하기

### 컴포넌트 스캔과 자동 의존관계 설정

- @Component : 어노테이션이 있으면 스프링 빈으로 자동 등록된다.
- @Controller: 컨트롤가 스프링 빈으로 자동 등록된 이유도 컴포넌트 스캔 때문이다.
- @Component를 포함하는 다음 어노테이션도 스프링 빈으로 자동 등록된다.
    - @Controller
    - @Repository
    - @Service
- 생성자에 @Autowired를 사용하면 객체 생성 시점에 스프링 컨테이너에서 해당 스프링 빈을 찾아서 주입한다. 생성자가 1개만 있으면 @Autowired는 생략이 가능하다.

![container2](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/container2.png "container2")
- memberService와 memberRepository가 스프링 컨테이너에 스프링 빈으로 등록되었다.
- 등록의 경우 @Service 와 @Repository로 등록
- 참고: 스프링은 스프링 컨테이너에 스프링 빈을 등록할 때, 기본으로 싱글톤으로 등록한다.(유일하게 하나만 등록해서 공유한다.) 따라서 같은 스프링 빈이면 모두 같은 인스턴스다. 설정으로 싱글톤이 아니게 설정할 수 있지만, 특별한 경우를 제외하면 대부분 싱글톤으로 사용한다. 
---
- DI(의존관계 설정)에는 필드 주입, setter주입, 생성자 주입, 이렇게 3가지 방법이 있다.
의존관계가 실행중에 동적으로 변하는 경우는 거의 없으므로 생성자 주입을 권장한다.
- 실무에서는 주로 정형화된 컨트롤러, 서비스, 리포지토리 같은 코드는 컴포넌트 스캔을 사용한다. 그리고 정형화 되지 않거나, 상황에 따라 구현 클래스를 변경해야 하면 설정을 통해 스프링 빈으로 등록한다.
- 주의: @Autowired를 통한 DI는 ‘helloController’, ‘MemberService’ 등과 같이 스프링이 관리하는 객체에서만 동작한다.
스프링 빈으로 등록하지 않고 내가 직접 생성한 객체에서는 동작하지 않는다.