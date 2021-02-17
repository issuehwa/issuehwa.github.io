---
title: "Spring: Maven + Spring + IntelliJ 프로젝트(2) - 컨트롤러, jsp(View) 생성"
excerpt: "메이븐과 스프링 최신 버전을 활용하여 스프링에 대해 공부하려 합니다."
categories:
  - SpringFramework
tags:
  - java
  - spring
  - backend
  - maven
  - intellij
author_profile: false
toc: true
toc_label: "컨트롤러, jsp 생성"
---

[이전 편: 생성, xml 설정](/springframework/02-spring-create) <br> <br> 

이전편에서 스프링 프로젝트 생성과 기본 xml설정을 해주었다. 
이제 컨트롤러와 View(jsp)파일을 생성하여 WAS(톰캣)에 올려 확인해 보도록 하자.

## 1. Controller

### 1) 패키지, 컨트롤러 생성
<figure class="half">
  <a href="{{ site.baseurl }}/assets/images/spring/spring-controller1.png"><img src="{{ site.baseurl }}/assets/images/spring/spring-controller1.png"></a>
  <a href="{{ site.baseurl }}/assets/images/spring/spring-controller2.png"><img src="{{ site.baseurl }}/assets/images/spring/spring-controller2.png"></a>
</figure>

- 먼저 dispatcher-servlet.xml에 정의한 패키지(디렉토리)에 맞춰 컨트롤러를 생성해준다.
- 나의 경우는 `com.spring.study` 패키지 내에 `HelloController`를 생성해 주었다.



### 2) 컨트롤러 정의

<figure>
  <a href="{{ site.baseurl }}/assets/images/spring/spring-controller3.png"><img src="{{ site.baseurl }}/assets/images/spring/spring-controller3.png"></a>
</figure>

- HelloController에는 @Controller 애노테이션을 class에 추가해 준다. 
- 그리고 @RequestMapping 애노테이션으로 class의 URL을 매핑해 준다. 나는 여기서 루트 ("/")로 매핑해 주었다.
- 다음으로 `index`라는 메서드에 ("/hello")를 매핑하여 `hostname:port/hello`로 접근 가능하도록 정의하였다.
- 모델앤뷰로 리턴하는 방식을 선택하였다. View에 `name`이라는 key로 `둘리`라는 value를 보냈다.

> HelloController.java 작성내용

```java
package com.spring.study;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@Controller
@RequestMapping("/")
public class HelloController {

    @RequestMapping(value = "/hello")
    public ModelAndView index(HttpServletRequest request, HttpServletResponse response) throws Exception {
        ModelAndView mav = new ModelAndView();

        mav.addObject("name", "둘리");

        return mav;
    }
}
```

## 2. View

### 1) jsp 파일 생성

<figure>
  <a href="{{ site.baseurl }}/assets/images/spring/spring-controller4.png"><img src="{{ site.baseurl }}/assets/images/spring/spring-controller4.png"></a>
</figure>

- 컨트롤러에서 정의한 `/hello` 에 맞춰 jsp 파일 생성
- viewResolver에 설정한 prefix, suffix 에 따라 아래와 같이 생성 (ex: /WEB-INF/jsp + /hello + .jsp)
- src > main > wabapp > WEB-INF > jsp > `hello.jsp` 파일 생성

### 2) jsp 작성

<figure>
  <a href="{{ site.baseurl }}/assets/images/spring/spring-controller5.png"><img src="{{ site.baseurl }}/assets/images/spring/spring-controller5.png"></a>
</figure>

- pageEncoding="UTF-8" 페이지의 문자 인코딩을 UTF-8로 지정해준다.
- `${name}` 컨트롤러에서 보낸 model정보를 EL방식으로 출력한다.

## 3. WAS 결과

<figure>
  <a href="{{ site.baseurl }}/assets/images/spring/spring-controller6.png"><img src="{{ site.baseurl }}/assets/images/spring/spring-controller6.png"></a>
</figure>

- 컨트롤러에서 `name`으로 보낸 `둘리`가 출력 되었다. 

## 참조
[https://chori84.tistory.com/32](https://chori84.tistory.com/32) <br>
[스프링 공식 사이트](https://spring.io/projects/spring-framework) <br>
[메이븐 리파지토리](https://mvnrepository.com/)




