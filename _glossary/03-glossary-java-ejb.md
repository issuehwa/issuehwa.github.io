---
title: "Java EJB"
permalink: /glossary/java/ejb/
excerpt: "Enterprise Java Bean"
last_modified_at: 2021-02-05
toc: ture
---

---

### EJB 란?

**기업환경의 시스템을 구현하기 위한 서버측 컴포넌트 모델**
{: .notice--info}

내용
:  Java EE의 자바 API 중 하나다. EJB는 어플리케이션의 비즈니스 로직을 가지고 있는 서버 어플리케이션이다. 주로 웹 시스템에서
JSP는 화면 로직을 처리하고, EJB는 비즈니스 로직을 처리하는 역할을 한다.


### EJB의 종류

1. 세션 빈 (Session Bean) : DB 연동이 필요 없음
2. 엔티티 빈 (Entity Bean) 
:  
 * 데이터베이스의 데이터를 관리하는 객체
 * Insert, Update, Delete, Select
 * DB 관련 쿼리는 자동으로 만들어지고 개발자는 고급 업무 처리에 집중할 수 있음
 * DB가 수정되면 코드 수정 없이 다시 배포 (설정 문서 만들어서 복사)
3. 메시지 구동 빈 (Message-driven Bean) : JMS로 빈을 날려줌

### EJB의 단점

- EJB의 혜택을 모두 얻기 위해서는 모든 기능이 다 필요하지도 않은 WAS를 구입해야 한다.
- 단위 테스트가 어렵다.
- 불필요한 메서드를 구현해야한다.
- 예외 처리가 번거롭다.
- 배포가 불편하다.


### EJB2.1 사용예제

불필요한 메서드를 구현
:  실제 비지니스 로직은 sayHello 뿐인데 EJB2.1에서는 ejbActivate(), ejbPassivate() ... 등의
메소드를 구현해야 한다.

```java
package com.habuma.ejb.session;
import javax.ejb.SessionBean;
import javax.ejb.SessionContext;

public class HelloWorldBean implements SessionBean {

    public void ejbActivate() {
    }

    public void ejbPassivate() {
    }

    public void ejbRemove() {
    }

    public void setSessionContext(SessionContext ctx) {
    }
    
    public String sayHello() {
        return "Hello World";
    }

    public void ejbCreate() {
    }
}
```

### 스프링의 등장

단순함과 유연성이 강조된 스프링이 등장

https://eminentstar.github.io/2017/07/05/tobi-spring-intro.html