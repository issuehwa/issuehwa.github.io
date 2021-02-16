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


- **pom.xml 추가사항**

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

**spring-webmvc의 \<type> 삭제하기**
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

- 이후 메이븐 프로젝트 depencency 업데이트 [이글](https://shydev.tistory.com/5)을 참조하면 된다.
  :  (*이클립스의 경우 프로젝트 마우스 오른쪽 클릭하면 메이븐 업데이트가 있다.)

### 3) 인텔리J와 이클립스 설정 파일 차이점 

| 관련 설정	                | IntelliJ              | 	Eclipse             |
|:--------------------------|:----------------------|:----------------------|
| 빈(bean) 설정	            | applicationContext.xml| root-context.xml      |
| 내부 웹 관련 처리 작업 설정	| dispatcher-servlet.xml| servlet-context.xml   |
| 톰캣(tomcat) 구동 관련 설정| web.xml	            | web.xml               |

## 참조사이트
[https://chori84.tistory.com/32](https://chori84.tistory.com/32) <br>
[스프링 공식 사이트](https://spring.io/projects/spring-framework) <br>
[메이븐 리파지토리](https://mvnrepository.com/)




