---
title: "NodeJs: NodeJs Web Server 구축하기"
excerpt: "Javascript"
categories:
  - NodeJs
tags:
  - npm
  - webserver
  - express
author_profile: false
toc: true
toc_label: "NodeJs"
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
 * 터미널 => node app.js 
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




## 참조
[https://webisfree.com/](https://webisfree.com/2017-10-30/nodejs%EB%A1%9C-%EA%B0%84%EB%8B%A8%ED%95%9C-%EC%9B%B9%EC%84%9C%EB%B2%84-%EA%B5%AC%EC%B6%95%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-%EB%B0%8F-%EC%98%88%EC%A0%9C%EB%B3%B4%EA%B8%B0)



