# 스프링 웹 개발 기초

## 정적 컨텐츠 - static

```html
<!DOCTYPE HTML>
<html>
<head>
    <title>static content</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
</head>
<body>
정적 컨텐츠 입니다.
</body>
</html>
```

- 그냥 파일을 고객에게 직접적으로 페이지 전달
- 스프링은 정적 컨텐츠 기능이 있음

![정적 컨텐츠](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/Static.png "정적 컨텐츠")
1. 웹브라우저에서 접속
2. 내장 톰캣서버를 통해 들어옴
3. 스프링 컨테이너에서 hello-static 관련 컨트롤러 확인
4. 없을 경우 스프링 부트의 정적 컨텐츠를 통해서 사용자에게 웹브루저로 전달

## MVC
```java
package boot.bootspring.controller;


import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class HelloController {

    @GetMapping("hello")
    public String hello(Model model){
        model.addAttribute("data", "spring!!");
        return "hello";
    }
    @GetMapping("hello-mvc")
    public String helloMvc(@RequestParam("name") String name, Model model){
        model.addAttribute("name", name);
        return "hello-template";
    }

}
```

```html
<html xmlns:th="http://www.thymeleaf.org">
<body>
<p th:text="'hello ' + ${name}" >hello! empty</p>
</body>
</html>
```
- Model
- View
- Controller

![MVC](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/MVC.png "MVC")
1. 웹브라우저 접속
2. 내장 톰캣 서버 접속해서 [localhost:8080/hello-mvc를](http://localhost:8080/hello-mvc를) 스프링에게 던짐
3. 스프링에서 컨트롤러에서 찾아보고 hello-mvc가 맵핑이 되어있는지 찾음
4. 있는 경우 메서드를 호출하고 리턴값과 모델을 값을 viewResolver로 전달
5. viewResolver에서 리턴값과 같은 템플릿 엔진을 처리해줌
6. 이후 엔진을 HTML로 변환 후 사용자 에게 전달
- 소스코드를 사용자가 확인한 경우 파라미터값이 사용자가 입력한대로 보임

## API

![API](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/Spring/API.png "API")
- @ResponseBody 이게 붙는다면 ViewResolver를 통하지 앉고 HttpMesaageConverter를 통해서 Json형식으로 바뀌고 사용자에게 Json그대로 보여드림.
