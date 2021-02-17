---
title: "Spring: Maven + Spring + IntelliJ 프로젝트(1) - 생성하기"
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
toc_label: ""
---

## 1. 개발 환경
- 메이븐 웹프로젝트
- 인텔리 J
- JAVA 8 (8u281)
- Spring Framework 5.3.3 (2021.2.10기준 최신 버전)
- Tomcat 9.0.6
- Servlet 4.0.1
- Github 버전관리 (*이후 개인 서비스 개발시 활용하기 위함)

## 2. 목적
- Spring Framework를 공부하기 위함
- 최신 기능을 따라해보기 위함
- 이후 개인 서비스에 활용하기 위함
- 스프링부트 공부 전 스프링프레임워크를 이해하기 위함

## 3. 실행
- 이 [블로그](https://chori84.tistory.com/32)를 참고하고 따라했다. 개발 환경은 현재 기준(2021.2) 최신버전으로 고쳐 적용하였다.<br>
- 블로그에서는 인텔리J에서 스프링을 받아 구조를 형성해 주는데, 최신버전 적용 및 Github 사용하여 다른 환경에서 쉽게 세팅하기 위해 메이븐으로 관리하였다.

### 1) 메이븐 웹프로젝트 생성
File > New > Project... > Maven 선택 <br>
archetype은 maven-archetype-webapp으로 선택

<figure class="half">
  <a href="{{ site.baseurl }}/assets/images/spring/maven-project1.png"><img src="{{ site.baseurl }}/assets/images/spring/maven-project1.png"></a>
  <a href="{{ site.baseurl }}/assets/images/spring/maven-project2.png"><img src="{{ site.baseurl }}/assets/images/spring/maven-project2.png"></a>
  <a href="{{ site.baseurl }}/assets/images/spring/maven-project3.png"><img src="{{ site.baseurl }}/assets/images/spring/maven-project3.png"></a>
</figure>

### 2) 메이븐 pom.xml 정의

[메이븐 리파지토리](https://mvnrepository.com/artifact/org.springframework/spring-webmvc/5.3.3)에서 검색하여 최신버전을 적용해 주었다.


#### ① pom.xml 추가사항

```xml
<properties>
    <org.springframework-version>5.3.3</org.springframework-version>
</properties>
    
<dependencies>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>${org.springframework-version}</version>
        <type>pom</type>
    </dependency>
</dependencies>
```

***spring-webmvc***는 spring-core, spring-context, spring-web, spring-aop, spring-beans, spring-expression에 대해 의존성이 있으므로 이 의존 라이브러리들이 자동으로 포함되어 집니다.
{: .notice--danger}

#### ② spring-webmvc의 \<type> 삭제하기

```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>${org.springframework-version}</version>
</dependency>
```

***\<type>pom\</type>***이 있으면 spring-webmvc에 관리되고 있는 의존 라이브러리만 가져온다. spring-webmvc라이브러리도 가져오기 위해 삭제 하였다.
{: .notice--danger}

#### ③ 아파치 메이븐 플러그인 버전 업데이트
[https://maven.apache.org/plugins/](https://maven.apache.org/plugins/) 참고하여,
2021년 2월 기준 최신버전을 적용하였다.


```xml
<build>
    <finalName>springStudy</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
        <plugins>
            <plugin>
                <artifactId>maven-clean-plugin</artifactId>
                <version>3.1.0</version>
            </plugin>
            <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
            <plugin>
                <artifactId>maven-resources-plugin</artifactId>
                <version>3.2.0</version>
            </plugin>
            <plugin>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
            </plugin>
            <plugin>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.0.0-M5</version>
            </plugin>
            <plugin>
                 <artifactId>maven-war-plugin</artifactId>
                 <version>3.3.1</version>
            </plugin>
            <plugin>
                <artifactId>maven-install-plugin</artifactId>
                <version>3.0.0-M1</version>
            </plugin>
            <plugin>
                <artifactId>maven-deploy-plugin</artifactId>
                <version>3.0.0-M1</version>
            </plugin>
            <plugin>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.2.0</version>
            </plugin>
        </plugins>
    </pluginManagement>
</build>

```

#### ④ 인텔리제이 메이븐 자동 업데이트
이후 메이븐 프로젝트 depencency 업데이트 [이글](https://shydev.tistory.com/5)을 참조하면 된다.
  :  (*이클립스의 경우 프로젝트 마우스 오른쪽 클릭하면 메이븐 업데이트가 있다.)

### 3) xml 파일 설정

<figure class="half">
  <a href="{{ site.baseurl }}/assets/images/spring/maven-project4.png"><img src="{{ site.baseurl }}/assets/images/spring/maven-project4.png"></a>
  <a href="{{ site.baseurl }}/assets/images/spring/maven-project5.png"><img src="{{ site.baseurl }}/assets/images/spring/maven-project5.png"></a>
</figure>

src > main > resources > spring 디렉토리(패키지)를 생성한다. <br>
`applicationContext.xml`, `dispatcher-servlet.xml` 파일 생성 <br>
src > main > webapp > WEB-INF > `web.xml` 파일 생성


#### ① 인텔리J와 이클립스 설정 파일 차이점 

| 관련 설정	                | IntelliJ              | 	Eclipse             |
|:--------------------------|:----------------------|:----------------------|
| WAS 구동 관련 설정         | web.xml	            | web.xml               |
| 공통 빈(bean) 설정	        | applicationContext.xml| root-context.xml      |
| 내부 웹 관련 처리 작업 설정	| dispatcher-servlet.xml| servlet-context.xml   |

- 파일명은 web.xml에서 지정할 수 있다.
- applicationContext.xml 와 dispatcher-servlet.xml 에서 겹치는 빈이 생길 경우
dispatcher-servlet.xml 의 빈을 사용하게 된다.

#### ② web.xml 설정
- WAS (톰캣)이 최초 구동 될때 web.xml을 참조하여 설정파일들을 불러온다.
- 설정을 위한 설정파일, DD(Deployment Descriptor) 배포 서술자라고 한다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--Root Context-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:/spring/applicationContext-*.xml</param-value>
    </context-param>

    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <!--DispatcherServlet / Front Controller-->
    <servlet>
          <servlet-name>appServlet</servlet-name>
          <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
          <init-param>
                <param-name>contextConfigLocation</param-name>
                <param-value>classpath:/spring/*-servlet.xml</param-value>
          </init-param>
    </servlet>
    <servlet-mapping>
          <servlet-name>appServlet</servlet-name>
          <url-pattern>/</url-pattern>
    </servlet-mapping>

    <!--UTF-8 인코딩 파라미터 설정-->
    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

</web-app>
```


#### ③ applicationContext.xml

- ContextLoaderListener에 의해 생성되는 Root WebApplicationContext를 정의한다.
- DispatcherServlet에서 참조할 수 있는 공통 빈을 정의한다. 
- 최초 생성시에 필요한 것이 없어 비워둔다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

</beans>
```


#### ④ dispatcher-servlet.xml 설정
- Front Controller로 사용자에 요청을 최초로 받아서 적절한 컨트롤러로 요청을 보내주는 역할을 합니다.
- `dispatcher`라는 단어는 영어로`보내다` 라는 뜻을 가지고 있다.
- context:component-scan을 활용하여 @Controller 만 스캔하여 빈으로 등록한다.
- viewResolver를 활용하여 String 타입의 뷰 이름으로 매핑한다. 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <!--component-scan: 애노테이션 Controller만 필터링-->
    <context:component-scan base-package="com.spring.study">
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller" />
    </context:component-scan>

    <!--View 리졸버: JSTL사용-->
    <bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="viewClass" value="org.springframework.web.servlet.view.JstlView" />
        <property name="prefix" value="/WEB-INF/jsp/" />
        <property name="suffix" value=".jsp" />
    </bean>
</beans>
```


## 참조
[https://chori84.tistory.com/32](https://chori84.tistory.com/32) <br>
[스프링 공식 사이트](https://spring.io/projects/spring-framework) <br>
[메이븐 리파지토리](https://mvnrepository.com/)




