---
title: "J2EE & Java EE & Jakarta EE"
permalink: /glossary/java/j2ee/
excerpt: "Java 2 Enterprise Edition, Java Platform Enterprise Edition"
last_modified_at: 2021-02-05
layouts_gallery:
  - url: /assets/images/glossary/java-ee-histroy.png
    image_path: /assets/images/glossary/java-ee-histroy.png
    alt: "Java EE History"
toc: ture
toc_icon: "cog"
---

---

### J2EE & Java EE & Jakarta EE 란?

**서버 개발에 필요한 자바 기능을 모아서 만든 표준**
{: .notice--info}

내용
:   
* J2EE를 SUN(Sun Microsystems)에서 만들어 시범적으로 스펙을 구현했지만, IBM, BEA, Oracle, HP, Iona등 여러 벤더사들도 그 스펙을 구현하고 개선하는 과정에 활발히 참여한다.
* J2EE는 5.0버전 이후 Java EE(Java Platform Enterprise Edition)로 개칭 되었다.
* Java EE스펙에 따라 제품으로 구현한 것을 웹 애플리케이션 서버 또는 WAS(Web Application Server)라 불린다. 외국에서는 AS (Application Server)라고 불린다.
* JVM(Java Virtual Machine)이라는 가상 머신을 통해 어떠한 플랫폼에서도 동일한 자바 소스 코드를 실행할 수 있다.
* 2017년 오라클에서 이클립스 재단으로 Java EE를 기부하였고, Java EE는 오라클의 상표로 남기에 새 이름 Jakarta EE로 개칭되었다.
* 자바 기술 관련 프로젝트로 자카르타 프로젝트가 있는 아파치 소프트웨어 재단은 이클립스 재단이 자카르타 EE를 사용하는데 흔쾌히 동의 했다.

### Java EE 대표적인 기능 스펙

- [EJB (Enterprise Java Beans)][glossary-java-ejb]

- Servlet

- JSP (Java Server Pages)

- JDBC (Java DataBase Connector)

- RMI (Remote Method Invocation)

- JNDI (Java Naming DirectoryInterface)

- JMS (Java Message Service)

[glossary-java-ejb]: {{ "/glossary/java/ejb/" }}


### History

{% include gallery id="layouts_gallery" caption="Java EE History Image" %}

|날짜             | 내용        |
|-----------------|--------------|
|1999년 12월 12일 | J2EE 1.2 SDK가 썬 마이크로시스템즈가 최초로 발표하였다.|
|                 |J2EE 1.3 스펙부터는 자바 커뮤니티 프로세스(Java Community Process;JCP)가 개발하였다.|
|2001년 9월 24일   |J2EE 1.3 |
|2002년 11월 11일 | J2EE 1.4 |
|2006년 5월 11일  | Java EE 5 스펙이 발표되었다. (J2EE에서 Java EE로 개칭)|
|2009년 12월 10일 | Java EE 6 스펙이 발표되었다.|
|2013년 5월 28일  | Java EE 7            |
|2017년 8월 31일  | Java EE 8            |
|2019년 9월 10일  | Jakarta EE 8 - Java EE 8과 완벽하게 호환            |
|                 | Jakarta EE 8 부터 이클립스 재단에서 관리 |
|2020년 11월 22일 | Jakarta EE 9 - javax.\*에서 jakarta.\* 네임 스페이스 변경.|

