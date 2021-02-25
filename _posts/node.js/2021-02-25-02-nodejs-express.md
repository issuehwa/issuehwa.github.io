---
title: "NodeJs: express-generator로 간단히 뼈대 만들기"
excerpt: "Express 애플리케이션 생성기"
categories:
  - NodeJs
tags:
  - npm
  - webserver
  - express
  - backend
author_profile: false
toc: true
toc_label: "express-generator"
---

<figure>
    <a href="{{ site.baseurl }}/assets/images/nodejs/express-1.png"><img src="{{ site.baseurl }}/assets/images/nodejs/express-1.png"></a>
</figure>

### 목적
```
Express 웹프레임워크로 간단히 Web Server를 구축을 했다. 복잡한 화면이 없고 버튼만 
구성해 주면 되는 되는 일이라서 그냥 html + js + css 로 구성하려고 했다.
웹서버만 활용하려고 프레임워크까지 얹은게 아까웠다.

그래서 Express 사이트를 보다보니 express-generator 라는 도구? 기능을 발견했다. 
전체적인 구조를 짜주는 녀석이였다. 큰 학습시간 없이 가능할 거 같았다.

아직 디자인이 없는 상태라 대충 개발환경까지만 세팅하는것이 목표이다.
```

### 개발환경
- NodeJs
- npm
- 비주얼스튜디오 Code
- OS: Windows10

### 설치, 설정 및 실행
<figure>
    <a href="{{ site.baseurl }}/assets/images/nodejs/nodejs-2.jpg"><img src="{{ site.baseurl }}/assets/images/nodejs/nodejs-2.jpg"></a>
</figure>

>모듈 패키지 관리자로는 NPM을 활용하였다.


#### 1. Express 설치

터미널을 열고 아래의 명령어를 실행해 줍니다.

```
npm install express-generator -g
```
- npm install 명령어 옵션 중 `-g`는 글로벌 패키지에 추가하는 내용입니다.
- 특정 위치에 설치할 경우 `--save` 옵션으로 대체하거나 npm5부터는
--save가 default 이므로 안 붙여줘도 됩니다.
- 글로벌로 설치 시 이후 새로운 프로젝트에서는 필요없습니다.

#### 2. Express 설정
`express -h` 또는 `express --help` 를 실행하면 아래와 같은 사용방법과 옵션을 보여준다. 
```
express -h

  Usage: express [options] [dir]

  Options:

        --version        output the version number
    -e, --ejs            add ejs engine support   
        --pug            add pug engine support
        --hbs            add handlebars engine support
    -H, --hogan          add hogan.js engine support
    -v, --view <engine>  add view <engine> support (dust|ejs|hbs|hjs|jade|pug|twig|vash) (defaults to jade)
        --no-view        use static html instead of view engine
    -c, --css <engine>   add stylesheet <engine> support (less|stylus|compass|sass) (defaults to plain css)
        --git            add .gitignore
    -f, --force          force on non-empty directory
    -h, --help           output usage information
```

- 템플린엔진으로 ejs, pug, handlebars를 지원한다.
- 템플릿엔진으로 handlebars engine을 선택하였다.

#### 3. handlebars 으로 프로젝트 생성

템플릿엔진으로 ejs, pug, handlebars 종류가 있는데, JAVA의 jsp와 비슷한 느낌이다.
나는 3가지 중 handlebars를 선택하였다. express에서 가장 추천은 pug(jade)를 하는 모양이지만
익숙하지 않은 모양새라서 일단 패스하였다.

```
// 이걸로 쓰면 경고메시지가 나온다.
express --hbs

// 변경된 방법 (사실 위에 처럼 사용해도 생성은 똑같이 해준다.)
express --view=hbs

// 현재 터미널이 열린 위치에서 하위로 디렉토리를 만들고 싶은 경우
express --view=hbs {디렉토리}
```

>위와 같이 실행하면 필요한 뼈대가 완성이 된다.

```
   create : public\
   create : public\javascripts\
   create : public\images\
   create : public\stylesheets\
   create : public\stylesheets\style.css
   create : routes\
   create : routes\index.js
   create : routes\users.js
   create : views\
   create : views\error.hbs
   create : views\index.hbs
   create : views\layout.hbs
   create : app.js
   create : package.json
   create : bin\
   create : bin\www

   install dependencies:
     > npm install

   run the app:
     > SET DEBUG=express-study:* & npm start
```
- 친절하게 다음 실행해야할 명령어도 적어준다. `npm install`

#### 4. npm install 필요한 모듈 설치

NPM을 활용하여 package.json에 있는 dependencies를 바탕으로 필요한 모듈을 설치한다.

```
npm install
```

- dependencies의 모듈과 의존 모듈을 모두 설치합니다.
- `node_modules` 폴더가 생성되고 그 아래로 모듈이 설치됩니다.

#### 5. 개발용 npm 스크립트 추가

```json
{
  "name": "express-study",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www",
    // 개발용으로 추가해준다.
    "watch": "nodemon --watch ./bin/www"
    
    // 처음에는 아래와 같이 사용하다가 바꿨다.
    // "watch": "node ./bin/www --ext .js, .hbs"
  },
  "dependencies": {
    "cookie-parser": "~1.4.4",
    "debug": "~2.6.9",
    "express": "~4.16.1",
    "hbs": "~4.0.4",
    "http-errors": "~1.6.3",
    "morgan": "~1.9.1"
  }
}
```

- `package.json` 파일을 수정해준다.
- 개발용으로 watch라는 이름으로 스크립트를 추가해준다.
- nodemon의 --watch 옵션을 활용하여 파일 수정시 서버를 재구동 없이 적용(핫리로드) 하였다.
- 요청사항을 로그로 확인 할 수 있다.


#### 6. 실행하기
```
npm run watch
```
- 위에서 작성한 npm 스크립트로 실행해 준다.
- 기본 [localhost:3000](http://localhost:3000)으로 설정되어 있다.
- bin > www 파일에서 port 을 수정할 수 있다.

>nodemon으로 구동시 확인할 수 있는 request 로그
<figure>
    <a href="{{ site.baseurl }}/assets/images/nodejs/express-2.png"><img src="{{ site.baseurl }}/assets/images/nodejs/express-2.png"></a>
</figure>

### 기타

- 라우터는 요청을 받고 처리하는 스프링의 Front Controller(Dispatcher-servlet)역할을 한다.
- 이 프로젝트에서 선택한 hbs가 view를 담당한다. 스프링의 jsp와 비슷하다.
- 레이아웃의 경우 스프링의 타일즈 같은 역할을 한다.
- 검색해보면 MVC 패턴으로 개량해서 사용을 한다. 
- [NodeJS 코딩 패턴 (Routes-Controllers-Services 구조)](https://gofnrk.tistory.com/65) 이 블로그에 간단히 적혀있어 좋다.
- 이번 서비스의 경우에는 간단히 표기만 하면 되기에 라우터에 컨트롤러, 모델 역할을 다 넣었다.



## 참조
[Express공식: https://expressjs.com](https://expressjs.com/ko/starter/installing.html)



