# Library
내가 사용한 라이브러리
- spring-boot-starter-web
- spring-boot-starter-thymeleaf

핵심라이브러리
- spring-boot-starter-web
    - spring-boot-starter-tomcat: 톰캣(웹서버)
    - spring-webmvc: 스프링 웹 mvc
- spring-boot-starter-thymeleaf: 타임리프 템플릿 엔진(View)
- spring-boot-starter(공통): 스프링 부트 + 스프링 코어 + 로깅
    - spring - boot
        - spring-core
    - spring-boot-starter-logging
        - logback,slf4j

테스트 라이브러리
- spring-boot-starter-test
    - junit: 테스트 프레임워크
    - mockito: 목 라이브러리
    - assertj: 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
    - spring-test: 스프링 통합 테스트 지원

### Welcome Page 만들기
```html
<!--main/resources/static/index.html -->
<!DOCTYPE HTML>
<html>
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
Hello
<a href="/hello">hello</a>
</body>

</html>
```

- 이 페이지에서 스프링 코드를 이해하고 활용할  줄 알아야 함.
https://spring.io/projects/spring-boot
- 스프링 부트는 static에 있는 static/index.html을 먼저 찾는다.

### THYMELEAF 템플릿 엔진 사용
thymeleaf 공식 사이트: https://thymeleaf.org/

#### 빌드하고 실행(터미널창 에서)
1. ./gradlew build
2. cd build/libs
3. java-jar hello-spring-0.0.1-SNAPSHOT.jar
4. 실행확인