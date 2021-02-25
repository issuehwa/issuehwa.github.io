---
title: "JSP"
permalink: /glossary/java/jsp/
excerpt: "Jsp (Java Server Pages)"
last_modified_at: 2021-02-19
toc: ture
toc_label: "JSP"
---

---

### 1. JSP(Java Server Pages) 란?

**HTML 코드에 Java 코드를 넣어 동적인 웹 페이지를 생성하는 기술**
{: .notice--info}

- Java 언어를 기반으로 하는 서버 사이드 스크립트 언어
- JSP는 WAS의 JSP Container를 통해 Java Servlet으로 변환 된다.
- [서블릿][servlet] 에서 확장된 기술을 사용한다.

#### 특징
- JSP는 다른 Java 파일과는 달리 컴파일 과정이 없다.
- 수정 하면 WAS(톰캣 등)에서 알아서 변환해서 보여준다.
- Java Beans 컴포넌트를 사용할 수 있다.
- `<% ~ %>`(* 스크립트릿-Scriptlet)로 JSP 영역을 표기하며 Web에서 소스로 보여지지 않는다.

#### Scriptlet 
```jsp
<%
    String str = "hello;    // java code
    out.println(str);
%>
```
- 스크립트릿은 자바코드로 서버단에서 먼저 처리 되어 `out`객체나 `<%= %>` 표현식을 통해
결과만 출력된다. 브라우저에서는 처리(해석)된 결과만 확인할 수 있다.

#### Jsp 지시자

```jsp
// page 지시자
<%@ page language="java" contentType="text/html; charset=UTF-8" 
pageEncoding="UTF-8"%>
<%@page import="java.util.ArrayList" %>

// include 지시자
<%@include file="sub.jsp" %>

// taglib 지시자
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```
- <%@ page language="java" %> @로 붙여준다.
- JSP페이지에 적용되는 정보를 적어준다.
- 사용할 자바 클래스를 임포트 할 수 있다.
- 다른 Jsp 파일을 불러올 수 있다.
- Jsp 문법 중 Action 또는 JSTL을 사용할 수 있게 한다.

#### Jsp 선언문

```jsp
<%!
 private int num = 1;
 private String str = "good";
 public int getNumber() {
    return this.num;
 } 
 public String getString() {
     return this.str;
 } 
%>
```

- <%! private int num = 1; %> !를 붙여준다.
- HTML 태그 위에 자바코드를 선언할 수 있다.
- 선언된 변수, 함수는 Jsp페이지 어느 곳에서도 참조 가능하다. 
- 선언문 <%! ~ %> 태그는 중복으로 사용 가능하다.

#### 표현식

```jsp
<%!
 private String str = "good";
%>
str에 담긴 단어는 <%= str %> 입니다.
```

- JSP 표현식은 ';' 세미콜론을 붙여주지 않는다. java파일로 변환시 out.print(); 자동으로 붙는다.


### 2. EL(Expression Language) & JSTL

**JSP 선언문 빼고는 거의 EL&JSTL로 작성하는 경우가 많다.**
{: .notice--info}

- EL(Expression Language)를 이용하면 `<%= %>` 등의 JSP 표현식을 사용하는 것보다 간단히
값을 가져올 수 있다.
- JSTL 사용하면 `<% %>` 같이 스크립트릿 태그를 사용해서 자바 코드를 작성하지 않아도 됩니다.



### 3. Jsp 컨테이너 란?
**Jsp를 Servlet으로 변환 하는 프로그램**
{: .notice--info}

#### 특징
- JSP 파일을 서블릿 소스로 변환 및 컴파일 까지만 담당한다.
- 변환된 서블릿은 [서블릿 컨테이너](/glossary/java/servlet/#2-서블릿-컨테이너-란)가 담당한다.

## 참조
[https://codeofenow.tistory.com/467](https://codeofenow.tistory.com/46) <br>
[http://blog.naver.com/](http://blog.naver.com/PostView.nhn?blogId=8x8x8x8x8x8&logNo=220866733906)<br>
[https://withcoding.com/41](https://withcoding.com/41)

<!--링크 참조-->

[servlet]: /glossary/java/servlet/ "Servlet"