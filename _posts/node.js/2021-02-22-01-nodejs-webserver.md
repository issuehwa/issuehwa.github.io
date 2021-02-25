---
title: "NodeJs: Web Server 구축하기"
excerpt: "Javascript Runtime"
categories:
  - NodeJs
tags:
  - npm
  - webserver
  - express
author_profile: false
toc: true
toc_label: "NodeJs Web Server"
---

<figure>
    <a href="{{ site.baseurl }}/assets/images/nodejs/nodejs-1.png"><img src="{{ site.baseurl }}/assets/images/nodejs/nodejs-1.png"></a>
</figure>

### 목적
```
개발한 서비스가 얼마 뒤 홈쇼핑에 나가게 되었다. 
홈쇼핑에서는 네트워크 환경이 끊키는 걸 감안하여, 
오프라인에서도 구동 가능하게 해달라는 요청사항이 있었다.

이 서비스는 웹서버가 필수 이기에 IIS, 아파치, Nginx 등 생각해보다가
NodeJs의 npm을 활용해서 간단히 web서버를 구축 해보려 한다.
```

### 개발환경
- NodeJs
- 비주얼스튜디오 Code

### NodeJs
- 구글 크롬 브라우저의 V8 javascript 엔진 기반의 javascript 런타임 이다.
: *`javascript runtime`이란 기존 브라우저에서만 실행되던 javascript를 브라우저 밖에서도 실행할 수 있는 환경을 말한다.
- 내장 HTTP 서버 라이브러리를 포함하고 있다.
- Javascript 언어로 서버 사이드에서 사용할 수 있다.

#### npm

<figure class="half">
    <a href="{{ site.baseurl }}/assets/images/nodejs/nodejs-2.jpg"><img src="{{ site.baseurl }}/assets/images/nodejs/nodejs-2.jpg"></a>
    <a href="{{ site.baseurl }}/assets/images/nodejs/nodejs-3.jpg"><img src="{{ site.baseurl }}/assets/images/nodejs/nodejs-3.jpg"></a>
</figure>

Node Packaged Manager, NodeJs 모듈 패키지 관리자 역할
{: .notice--info}

- NodeJs로 만들어진 모듈을 웹에서 받고 설치 및 업데이트 관리
- `yarn` 이라는 facebook 진영에서 만든 패키지 매니저도 있다.


### 실행방법

#### 1. app.js파일 생성 (*네이밍은 마음대로)
>NodeJs에서 동작 될 어플리케이션 js파일을 생성하고 아래 코드를 넣습니다.

```javascript
/**
 * 구동방법 
 * 해당 포트로 웹서버 구동 확인 가능
 */
const http = require('http');
const port = 8282;
http.createServer((request, response) => {
    console.log('HTTP server start on port ' + port);

    response.writeHead(200, {'Content-type': 'text/plan'});
    response.write('Hello Node World!');
    
    response.end();
}).listen(port);
```

#### 2. NodeJs 웹서버 구동
>터미널에서 명령어 node app.js(생성한 어플리케이션)을 적어주시면 됩니다. 

```terminal
node app.js
```

#### 3. 결과
<figure>
    <a href="{{ site.baseurl }}/assets/images/nodejs/nodejs-4.png"><img src="{{ site.baseurl }}/assets/images/nodejs/nodejs-4.png"></a>
</figure>


### Express framework

- NodeJs에서 가장 많이 쓰이는 프레임워크 이다. 
- Java의 스프링, PHP의 라라벨, 파이썬의 django와 같은 개념이다.
- NodeJs의 핵심 모듈 `http`, `Connect` 컴포넌트를 기반으로 한다.

#### 1. 설치

>npm 명령어를 활용하어 설치한다.

```
// 디펜더시에 추가
npm install express --save

// 디펜더시에 추가하지 않음
npm install express --no-save 
```

#### 2. app.js 내용 수정

```javascript
/**
 * Express는 node로 웹서버 환경 구축시 가장 많이 사용되는 프레임워크
 */
const express = require('express'); // express 모듈 추가하기

const app = express();
const port = 8282;
const path = require('path');

app.use('/', (request, response, next) => {
  response.sendFile(path.join(__dirname + '/view/index.html'));
});

app.listen(port, function(err) {
  console.log('Connected port - ' + port);
  if (err) {
    return console.log('Found error', err);
  }
})
```

#### 3. index.html 파일 작성

Express를 활용하여 "/" 루트 라우팅에서 보여줄 index.html 파일을 생성한다.
`view` 폴더 아래에 `index.html` 생성하였다.

<figure>
    <a href="{{ site.baseurl }}/assets/images/nodejs/nodejs-5.png"><img src="{{ site.baseurl }}/assets/images/nodejs/nodejs-5.png"></a>
</figure>

>html 작성내용

```html
<html>
    <body>
        <h1>Hello Express World!</h1>
    </body>    
</html>
```

#### 4. NodeJs 웹서버 구동

>터미널에서 명령어 node app.js을 적어주시면 됩니다. 

```terminal
node app.js
```

#### 5. 결과

<figure class="half">
    <a href="{{ site.baseurl }}/assets/images/nodejs/nodejs-6.png"><img src="{{ site.baseurl }}/assets/images/nodejs/nodejs-6.png"></a>
    <a href="{{ site.baseurl }}/assets/images/nodejs/nodejs-7.png"><img src="{{ site.baseurl }}/assets/images/nodejs/nodejs-7.png"></a>
</figure>


#### 6. 정적 파일 제공: express.static()

이미지, CSS 파일 및 JavaScript 파일과 같은 정적 파일을 제공하기 위한 Express 
기본 제공 미들웨어 함수 express.static를 사용한다.
{: .notice--info}

>public 이라는 이름의 디렉토리에 포함된 이미지, CSS파일 등 제공하는 방법

```javascript
app.use(express.static('public'));
app.use(express.static('files'));
```

- 중복으로 여러번 호출 가능
- 별도의 마운트 경로가 없을 시 "/"에서 접근 가능

**접근 예시**

```html
http://localhost:포트/images/kitten.jpg
http://localhost:포트/css/style.css
http://localhost:포트/js/app.js
http://localhost:포트/images/bg.png
http://localhost:포트/hello.html
```

>마운트 경로 지정: static 이라는 가상 경로 

```javascript
// 상대 경로
app.use('/static', express.static('public'));

// 절대 경로
app.use('/static', express.static(__dirname + '/public'));
```

- use 메서드에 첫번째 인자로 `'/static'` 등의 경로 string 값을 주면 
가상 경로로 접근가능
- express.static 함수에 제공되는 경로는 node 프로세스가 실행되는 디렉토리에
대해 상대적입니다. Express 앱을 다른 디렉토리에서 실행 하는 경우 `__dirname`을 사용하여
절대 경로를 사용하는 것이 더 안전합니다.

**접근 예시**

```html
http://localhost:포트/static/images/kitten.jpg
http://localhost:포트/static/css/style.css
http://localhost:포트/static/js/app.js
http://localhost:포트/static/images/bg.png
http://localhost:포트/static/hello.html
```



## 참조
[블로그: https://webisfree.com/](https://webisfree.com/2017-10-30/nodejs%EB%A1%9C-%EA%B0%84%EB%8B%A8%ED%95%9C-%EC%9B%B9%EC%84%9C%EB%B2%84-%EA%B5%AC%EC%B6%95%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-%EB%B0%8F-%EC%98%88%EC%A0%9C%EB%B3%B4%EA%B8%B0)<br>
[Express공식: https://expressjs.com](https://expressjs.com/ko/starter/installing.html)



