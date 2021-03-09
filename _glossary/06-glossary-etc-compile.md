---
title: "Compile & Build & Deploy"
permalink: /glossary/etc/compile/
excerpt: "컴파일, 빌드, 배포"
last_modified_at: 2021-03-09
toc: ture
toc_label: "컴파일 & 빌드 & 배포"
---

---

### 1. 컴파일(Compile)

**개발자가 작성한 소스 코드를 컴퓨터가 이해할수 있는 기계어(바이너리 코드)로 변환하는 작업**
{: .notice--info}

- 컴파일러(Compiler): 소스 코드를 기계어로 변환(번역)하는일을 하는 프로그램
- 자바일 경우 JVM에서 실행 가능한 바이트 코드 형태의 클래스 파일이 생성된다.
- ex) Test.java => 컴파일 => Test.class

### 2 링크(Link)

**분리된 소스코드를 연결하여 실행 파일로 만드는 작업**
{: .notice--info}

- 링커(Linker) : 소스 코드를 연결하는 프로그램
- 분리되어 있는 소스 코드를 다시 연결하는 역할을 한다.
- 라이브러리, 리소스 등 사용 가능하도록 실행파일로 만든다.
- ex) *.jar, *.war, *ear

### 3. 빌드(Build)

**컴파일과 링크 과정을 합쳐진 것을 빌드라 한다.**
{: .notice--info}

- 자바 빌드 도구 : ant, Maven, gradle 등이 있다.
- 빌드 도구을 사용하면 의존성 관리가 쉬워진다.
- 요즘은 `gradle`이 대세인듯 하다.


### 4. 배포(Deploy)

**빌드된 실행파일을 사용자가 접근 가능한 환경에 배치 하는 것**
{: .notice--info}

- 웹의 경우 WAS(톰캣)에 올려 사용자(브라우저)가 접근 할 수 있도록 한다.
- *.exe 실행파일로 사용자에게 전달 할 수도 있다.

### 참고

[오픈튜토리얼: https://www.opentutorials.org/module/1594/9734](https://www.opentutorials.org/module/1594/9734)<br>
[우아한테크: https://www.youtube.com/watch?v=JgRCaVwkPE8](https://www.youtube.com/watch?v=JgRCaVwkPE8)
