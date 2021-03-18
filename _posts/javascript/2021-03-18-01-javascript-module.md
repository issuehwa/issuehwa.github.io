---
title: "JavaScript: module 특징"
excerpt: "JavaScript 모듈 사용법 및 특징"
categories:
  - JavaScript
tags:
  - javascript
  - frontend
  - es6
author_profile: false
toc: true
toc_label: "JavaScript 모듈"
---

### 개발환경
- IDE: IntelliJ 2018
- Typescript v4.2.3
- Javascript
- Nodejs
- 구글맵 API

### 발단
```
이번에 회사로 드론관련 하여 문의가 들어왔다.
기술 검토를 하기 위해 검증이 필요하여, 
얼마전 사용한 Nodejs를 활용하기로 했다.

기본적인 것은 구글맵 API를 활용하고,
그외 필요한 기술은 커스텀 해보기로 한다.

구글 API를 보니 javascirpt, Typescript 예제를 둘다 제공한다.
이왕 하는거 Typescript를 써보기로 하고 세팅하였다.
```

### 구조
```
-- assets  
 ㄴ css   
 ㄴ js    ------------- .ts파일에서 트랜스파일된 .js 파일
 ㄴ ts    ------------- 작성할 .ts 파일
-- node_modules
index.html  ----------- 결과 화면
server.js   ----------- Nodejs 웹서버
tsconfig.json  -------- 타입스크립트 설정
package.json  --------- npm 설정 파일
```

- 위와 같이 구조를 간단히 짜고 작업을 시작하였다.
- 결론 부터 말하면 `index.html`에서 `.js`를 module로 사용하는 게 
구글API 콜백과 문제가 되었다.

### 문제 발생
```
최초 개발은 하나의 .ts파일로 해결하였다.
필요한 핵심 기능의 가능여부를 확인하고,

구글API와 분리하기 위해 별도의 .ts파일을 생성하고,
기본 .ts에서 커스텀.ts 파일을 import하면서 error를 뱉어낸다.

해결하면서 알게 된 사실을 몇 가지 적어보려한다.
```

### 용어

#### 1) module
- 예전 자바스크립트는 정적인 html를 동적으로 움직이기 위해 사용하였다면, 
점차 단독으로 사용 가능한 수준까지 발전하게 되었습니다. 간단한 예를 들자면
이번 프로젝트에 채용한 Nodejs가 있습니다.

- 정통적인 js파일을 html에 `<script type="text/javascript"></script>` 태그안에
작성하거나 로드하여 사용했습니다. 그래서 로드 하는 순서도 중요하지요. 
jQuery만 하더라도 코어, datepicker등 사용할 추가 라이브러리, 3rd 파티 라이브러리 순으로
로드했어야 합니다. 
   
- 그렇게 사용하던 것이 backend로도 사용하면서 js 안에서 js파일을 로드해야하는 일이 생기게 됩니다.

- es6 부터 export, import가 생기면서 모듈을 쉽게 생성, 로드할 수 있게 되었습니다.
    
#### 2) import VS require             
- javascript ES6부터 제공하는 문법이 `import` 입니다.
- ES6 이전에 js의 모듈화를 정의하던 CommonJS에서 제공하는 문법이 `require` 입니다.
- Nodejs가 CommonJS를 모듈 명세를 따르고 있습니다.
- 둘다 혼용해서 사용할 수 있지만, 하나로 통일하는 것을 추천한다.


### 증상 1: 임포트한 모듈 접근 안됨

>index.html

```html
// index.html
<head>
    <script src="./assets/js/index.js"></script>
</head>

<body>
    <div id="map"></div>
</body>

// 구글맵 API script
// callback=initMap 콜백을 받는 함수를 적어주는 부분이 있다.
<script
  src="https://maps.googleapis.com/maps/api/js?callback=initMap"
  async defer
></script>
```

>index.ts

```typescript
// index.ts
import {test} from './google.map.js';

let map: google.maps.Map;

function initMap(): void {
  map = new google.maps.Map(document.getElementById("map") as HTMLElement, {
    zoom: 15,
    center: { lat: 37.54288394810494, lng: 126.98903736942411 },
  });
  
  // import한 test파일 간단히 사용해보자
  console.log(test);
}
```

>에러

```
Cannot use import statement outside a module
```
- 아래 에러를 뱉어내고 import한 부분에서 멈춘다.
- html에 잘보면 `<script src="./assets/js/index.js"></script>` 이부분이 있는데,
`type="module"`을 추가해 주어 이 .js파일이 모듈이라는 것을 알려준다.


#### 증상 2: 콜백함수 에러

>index.html 수정 : type="module" 추가

```html
// index.html
<head>
    <script type="module" src="./assets/js/index.js"></script>
</head>
.
.
.
```

>에러

<figure>
  <a href="{{ site.baseurl }}/assets/images/javascript/javascript-01.png"><img src="{{ site.baseurl }}/assets/images/javascript/javascript-01.png"></a>
</figure>

- 모듈화 되면서 외부에서 모듈 내부 함수를 접근하지 못하게 된다.
- 구글맵API에서 콜백함수를 호출하는 부분을 접근하지 못하여 생긴 에러이다.


### 해결방안

**콜백함수만 별도로 작성 or 로드, 별도의 모듈로 구분**
{: .notice--info}

- 여러 해결방법이 있겠지만 간단하게 생각했다.
- 콜백함수만 별도로 로드하여, 콜백시 호출할 수 있게 해주었다.
- 이후 모듈내에서는 이벤트리스너를 걸어 이벤트를 처리했다.

>index.html

```html
<!-- 구글맵 콜백용 -->
<script src="./assets/js/google.map.js"></script>
<!-- 커스텀 모듈 -->
<script type="module" src="./assets/js/custom.js"></script>
```

>google.map.ts

```typescript
let map: google.maps.Map;

// 구글맵 콜백 함수
function initMap(): void {
  map = new google.maps.Map(document.getElementById("map") as HTMLElement, {
    zoom: 15,
    center: { lat: 37.54288394810494, lng: 126.98903736942411 },
  });
}
```

>이벤트 리스너

```typescript
// ex) 이벤트리스너 처리
let btnInvisible = document.getElementById("invisible") as HTMLElement;
btnInvisible.removeEventListener('click', invisibleRectangle);
```

### 결론
- 이전 Vue 프로젝트에서 import와 require를 활용해서 라이브러리, store등을 가져왔는데,
차이점을 이제야 알게 되었다.
- Nodejs, Vue, AngularJs 등 javascript 라이브러리, 프레임워크가 늘어나는 환경에서
기초 중에 하나를 알게 된거 같아 좋았다.
- 타입스크립트, 바벨, 웹팩 등 그동안 신경 쓰지 않았던 개발환경을 좀 더 공부해 보아야겠다.

## 참조
[네이버D2: https://d2.naver.com/helloworld/12864](https://d2.naver.com/helloworld/12864)<br/>
[https://www.daleseo.com/js-module-require/](https://www.daleseo.com/js-module-require/)


