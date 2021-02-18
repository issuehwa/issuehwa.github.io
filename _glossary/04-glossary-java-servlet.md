---
title: "Servlet"
permalink: /glossary/java/servlet/
excerpt: "서블릿 (Servlet)"
last_modified_at: 2021-02-18
toc: ture
toc_label: "Servlet"
---

---

### 1. 서블릿(Servlet) 이란?

**사용자 요청(HTTP)에 Java로 로직 처리 후 HTML 형식으로 응답**
{: .notice--info}

 - [Java EE(J2EE)][JavaEE]에서 제공하는 Servlet 클래스의 구현 규칙을 지킨 자바 프로그램이다.
 - URL주소에 매핑된 자바클래스를 호출(요청)하여, 자바로 짜여진 코드를 브라우저에서 보여줄 수 있는 HTML로 변환(응답)하여 볼 수 있게 만들어주는 역할을 한다.
 - Java로 구현된 CGI(Common Gateway Interface) 라고 이야기 함.
 - 웹에서 Java프로그래밍을 구현하기 위해 탄생 함.

#### 특징
 - .java 확장자, 자바 클래스로 컴파일 된다.
 - MVC 패턴(스프링)에서 Controller로 이용한다.
 - 서블릿 컨테이너에 의해 Servlet이 관리된다.
 - Java 코드 안에 HTML 코드가 포함된다.
 
#### 동작 방식

1. Web Server 에서 받은 사용자 요청(HTTP Request)을 Servlet Container 로 전송
2. 요청 받은 Servlet Container 는 HttpServletRequest, HttpServletResponse 객체 생성
3. web.xml(배포 서술자)에 정의된 내용을 바탕으로 요청에 매핑된 서블릿의 생성자 호출
4. Servlet Container 에서 요청 처리할 Thread 생성
5. 서블릿 service() 메소드 호출, 사용자 메소드(GET, POST)에 따라 doGet(), doPost() 호출
6. 서블릿이 요청에 따른 페이지 생성 후 HttpServletResponse 객체에 담아 전송
7. Servlet Container 에서 HTTP Response 로 바꿔 Web Server 에 전송
8. HttpServletRequest, HttpServletResponse 객체 소멸 후 Thread 종료

#### 기본 구성

```java
// 보통 HttpServlet 상속하여 쓴다.
public class TestServlet extends HttpServlet{
    
    protected void doGet(HttpServletRequest request, HttpServletResponse response) 
        throws ServletException, IOException {
        // TODO
        // 할일~~ 샬롸 샬롸~
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response) 
        throws ServletException, IOException {
        // 포스트로 온 요청도 doGet() 메서드 호출로 돌린다.
        doGet(request, response);
    }
}
```

### 2. 서블릿 컨테이너 란?

**서블릿을 서버에서 실행하기 위한 서버 프로그램**
{: .notice--info}

- Web Server 는 서블릿 자체를 실행하지 못하므로 JVM이 내장된 서블릿 컨테이너가 필요하다.
- 대표적인 서블릿 컨테이너(웹 컨테이너)에 Tomcat 이 있다.

#### 특징
- HTTP 요청을 받아 서블릿을 실행하고 생명주기를 관리한다.
- 서블릿과 웹서버가 통신할 수 있는 방법을 제공한다.
- 멀티 스레딩을 지원하여 사용자의 다중 요청을 처리한다.

#### 매핑방법

- 3.0 이하 버전에서는 `web.xml`에 정의
- 3.0 이상 버전에서는 `@WebServlet` 애노테이션도 지원함

>방법 1: xml

```xml
<servlet>
    <servlet-name>testServlet<servlet-name>
    <servlet-class>com.spring.study.TestServlet<servlet-class>
</servlet>
<Servlet-mapping>
    <servlet-name>testServlet</servlet-name>
    <url-pattern>/test</url-pattern>
</Servlet-mapping>
```

>방법 2: 애노테이션

```java
@WebServlet("/test")
public class TestServlet extends HttpServlet{
  //do
  //someting
}
```

## 참조
[https://galid1.tistory.com/487](https://galid1.tistory.com/487) <br>
[https://ddo-o.tistory.com/77](https://ddo-o.tistory.com/77)


<!--링크 참조-->

[JavaEE]: /glossary/java/j2ee/ "J2EE&JavaEE"