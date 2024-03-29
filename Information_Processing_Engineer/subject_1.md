# 소프트웨어 설계

## 1. 애자일 방법론
- 고객 요구사항 변화에 중심
- 고객 요구사항 최우선이기에 **유연한 방법론이기에 문서 중심이 아님.**
- XP(익스트림 프로그램)은 애자일 방법론을 통한 프로그래밍 기법 중 하나
- 주요가치
    - 의사소통
    - 피드백
    - 단순성
    - 존중
    - 용기

## 2. UI설계원칙
- **오류를 숨겨서는 안됨.**
- 직관성
- 유효성
- 학습성
- 유연성

---
## 3. 요구사항 유형
- 기능적 요구사항: 실제 시스템 수행에 필요한 사항들
    - ex) 조회/인출/입금/송금
- 비기능적 요구사항: 성능, 품질, 보안, 안정성 등 **실제 수행에 보조적인 지표**
    - ex) 모든 화면이 사용자에게 3초 이내로 보여져야 함.
> 기능이 있냐 -> **기능적**  

>성능이 이정도는 되야하지 않냐 -> **비기능적**

#### 3-1. 요구사항 개발 프로세스
- 도출/추출 -> 분석 -> 명세 -> 확인/검토(검증)

#### 3-2. 요구사항 검토 방법
- 워크 스루(Walk Through): 
    검토 회의 전 요구사항 **명세서를 미리 배포**해 사전 검토 후 
짧은 회의로 결함 발견.  
-> Walk: '걷다' 의미인 만큼 걸을 때 전단지 나눠주면서 보듯이 **가볍게 결함을 발견**
- 인스벡션(Inspection): 명세서 작성자를 제외한 다른 **전문가들이 명세서를 확인**하면서 결함을 발견.  
-> 전문가가 등장하기에 꽤나 무거운 느낌의 검사
---
## 4. CASE 도구
#### Computer Aided Software Engineering 도구로, 컴퓨터의 도움을 받는 요구사항 검증 방법
- S/W 라이프 사이클 전 단계의 연결
- 그래픽 지원
- 다양한 소프트웨어 개발 모형 지원
- 다이어그램 작성 가능
- 개발자 협업에 도움

## 5. 럼바우 객체지향 분석 기법

- 객체 모델링(Object Modeling): 객체 다이어그램, 시스템에서 요구하는 객체를 찾고 객체들 간의 관계를 정의하며 가장 중요하게 선행 되어야 함.
- 동적 모델링(Dynamic Modeling): 상태 다이어그램, 시간의 흐름에 따라 객체들 사이의 제어 흐름, 동작 순서등의 동적인 행위 표현
- 기능 모델링(Funtional Modeling): 자료 흐름도(DFD), 프로세스들의 자료 흐름 중심으로 처리 과정 표현

> **객체 -> 동적 -> 기능** 순서로 외워야 함.  
    > - 객체 : 모델링, 객체  
    > - 동적 : 상태, 동작 순서  
    > - 기능 :  자료흐름도(DFD)  

## 6. 객체 지향 기법
- 캡슐화(Encapsulation)
    - 데이터와 함수를 하나로 묶는 것
    - 재사용성 증가, 오류 파급 효과 감소
    - 인터페이스 단순화, 객체 간 결합도 낮아짐
- 정보 은닉(Information Hiding)
    - 다른 객체에서 자신의 정보를 숨기고 자신의 연산만을 통해 접근
- 상속(Inheritance)
    - 상위(부모) 클래스 속성 및 연산을 하위(자식) 클래스가 물려받는 것
- 추상화(Abstraction)
- 다형성(Polymorphism)

## 7. 소프트웨어 생명 주기
- 폭포수 모델: 고전적으로 전통적인 모델, 순차적인 개발이 특징, 이전 단계를 다시 보기 어려움.
- 나선형 모델: **위험 분석 및 위험 최소화**가 목적  [계획 -> 위험 분석 -> 개발 및 검증 -> 고객 평가 과정]  
이와 같은 과정을 여러번 반복하면서 리스크를 줄이는게 특징
- 프로토타입 : 견본/시제품을 통해 최종 결과 예측,  
인터페이스 중심, 요구사항 변경 용이
- HIPO(Hireachy Input Process Output) : 하향식 설계이며 가시적, 총체적, 세부적 다이어그램 구성, 기능과 자료 의존 관계 동시 표현

## 8. 하향식 설계, 상향식 설계
- 하향식 설계 : 절차 지향(순차적)  
-> 최상위 컴포넌트 설계 후 하위 기능 부여
- 상향식 설계 : 객체 지향  
-> 최하위 모듈부터 설계 후 이들을 결합해 검사/ 기능추가 어려움   
~~회사에서 상사에게 무언가 요구하는게 어렵듯 상향식 설계는 무언가 기능을 추가하기 어려움.  
반대로 위에서 내려오는건 수시로 변경되기에 올라가는 것 보다 기능 추가나 변화가 쉬운 편.~~

## 9. 자료 흐름도 DFD
- 시스템이나 프로세스 내 정보의 흐름을 시각적으로 나타내는 도표
     - 의미와 도형 연결
     - Process: 원
     - Data flow: 화살표
     - Data source: 직선(단선/이중선)
     - terminator : 사각형  
     > 삼각형은 쓰이지 않음

---
## 10. 다이어그램
- 구조, 정적 다이어그램 종류  
  ->  클래스, 객체 , 컴포넌트, 배치, 복합체, 패키지
- 행위, 동적 다이어그램 종류  
  -> 유스케이스, 순차, 커뮤니케이션, 상태, 활동, 타이밍, 상호작용 개요

#### 10-1. 행위 동적 다이어그램
- 유스케이스 다이어그램: 사용자 요구를 분석
- 순차 다이어그램: 시스템, 객체들이 주고 받는 메세지를 표현하며 액터, 객체, 생명선, 메세지, 제어 삼각형 등 존재
> 액터란? **시스템과 상호작용**하는 사람이나 다른 시스템에 의한 역할
> - 사용자 액터 : 기능을 요구하는 대상이나 시스템의 수행결과를 통보받는 사용자
> - 시스템 액터 : 본 시스템과 데이터를 주고 받는 연동 시스템

## 11. 디자인 패턴 GOF(Gang of Four)
디자인 패턴은 **자주 발생하는 문제를 해결하기 위한** 반복적 해결 방법.  
주로 어떤 패턴에 어떤게 속하는지 나옴.  
간단하게 무슨 패턴인지 알아두면 베스트.

#### 11-1. 생성패턴
>   - 추상 팩토리(Abstract Factory) : 연관 객체 그룹 생성 후 추상적 표현

>   - 빌더(Builder) : 조립, 객체 생성

>   - 팩토리메서드(Factory Method) : 객체 생성을 서브클래스에서 결정해서 생성

>   - **프로토타입(Prototype) : 원본 객체 복제해서 생성**

>   - **싱글톤(Singleton) : 필요시 하나의 객체만 생성할 수 있게(DB연결 등)**

**팩토리, 빌더가 나오면 일단 생성이다.**

#### 11-2. 구조 패턴
>   - 어댑터(Adaptor)  
-> 비호환 인터페이스에 호환성 부여할 수 있는 구조로 구성

>   - 브릿지(Bridge)  
-> **독립적 확장**이 가능하게 구조 구성  
---서로 연결하는 역할이 아니다.---

>   - 컴포지트(Composite)  
->  복합, 단일 객체 구분없이 사용할 수 있게 구조 구성

>   - 데코레이터(Decorator)  
-> 상속 없이 확장할 수 있는 구조 구성

>   - 퍼사드(Facade)  
-> 상위 인터페이스 구성 후 서브 클래스 기능 사용할 수 있게 구조 구성

>   - 플라이웨잇(Flyweight)  
-> 인스턴스 공유 및 메모리 절약할 수 있게 구조 구성

>   - **프록시(Proxy)**  
-> 접근이 힘든 **객체를 연결하는 인터페이스 역할**할 수 있게 구조 구성

#### 11-3. 행위 패턴
>   - **메멘토(Memento)**
>   - **옵저버(Observer)**
>   - 상태(state)
>   - **전략(Strategy)**
>   - **템플릿(Template Method)**
>  - Command
>  - Interpreter
>  - Iterator
>  - Mediator
>  - Visitor

## 12. 코드의 종류
- 순차 코드  
-> 최초의 자료부터 일정한 일련번호를 부여하는 방법
- 블록코드  
-> 공통 블록으로 구분하고 블록내에 일련번호를 부여하는 방법
- 10진 코드  
-> 0~9 까지 10진 분할해 코드 부여
- 연상 코드  
-> 명칭이나 관계 있는 숫자, 문자 등을 부여
- 표의 숫자 코드  
-> 항목의 물리적 성질 등 그대로 부여(32인치 모니터 등)
- 합성코드  
-> 위 코드 중 2개 이상을 조합해 적용하는 방법

## 13. 자료사전 기호
- '=' 정의
- '+' 연결
- '{}' 반복
- '[]' 선택
- '()' 생략
- '**' 주석
---
~~출처 :  https://codingdodo.tistory.com/83~~


