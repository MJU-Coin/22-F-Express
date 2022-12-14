# Express.js

## 정의

- Node.js를 위한 웹 프레임워크의 하나

## 기능

- 수많은 HTTP 메소드 및 middleware을 통해 쉽고 빠르게 API 작성이 가능(여러 API를 제공)

## 개요

![](https://velog.velcdn.com/images/kakasoo/post/15aea058-859f-4483-9281-df4c6436862b/ch1_pic7.png)

- Route로 연결되면 각 Layer가 가진 handler을 실행한다

# express generator

- express의 기본적인 구성을 만들어주는 기능

# Routing
- 한 파일에 여러기능을 다 넣으면 보안문제, 가독성, 디버깅 등이 어려워짐
- URL 및 특정 HTTP 요청 메소드(GET, POST)인 특정한 end point에 대한 클라이언트 요청에 어플리케이션이 응답하는 방법을 결정하는 것


## 예제

```jsx
import express from "express";
const app = express();

app.get('/', function(req, res) {
  res.send('hello world');
});
```

- 홈 페이지에서는 hello world로 응답

```jsx
app.put('/user', function (req, res) {
  res.send('Got a PUT request at /user');
});
```

- /user 라우터에 대한 put 요청에 대한 응답

## 라우트 핸들러

- middle ware와 비슷하게 작동하는 여러 콜백 함수를 제공하여 요청을 처리할 수 있다
    - 추가적으로  next(’route’)를 호출해 나머지 라우트 콜백을 우회할 수 있음
        - 라우트에 대한 사전 조건을 지정한 후 , 현재의 라우트가 필요 없을 경우 제어를 후속 라우트에 전달 할 수 있다
- 형태
    - 함수나 함수 배열의 형태 or 둘을 조합한 형태로 나타남
- 하나의 콜백 함수는 하나의 라우트를 처리할 수 있다

```jsx
app.get('/example/a', function (req, res) {
  res.send('Hello from A!');
});
```

- 두개 이상의 콜백함수가 하나의 라우트를 처리할려면 반드시 next 오브젝트를 지정해야 한다

```jsx
app.get('/example/b', function (req, res, next) {
  console.log('the response will be sent by the next function ...');
  next();
}, function (req, res) {
  res.send('Hello from B!');
});
```

# Method

### get

- 주소에 값이 나옴

### post

- 주소에 값이 안나옴
    - 너무 긴 내용은 post로 넘겨줘야 한다
- binary 형태의 데이터도 post로 넘겨준다

### path

- URL주소의 path’/’로 데이터를 구분하여 가져오는 것
- 문법은 /:파라미터명 이다
- params에 담겨온다
- 어떤 파라미터에 데이터를 받을지 path에 표시하기에 한번에 어떤 데이터를 받는지 파악 가능

```jsx
app.get('/test/:email',(req,res)=>{
testjson.email = req.params.email
res.json(testjson)
})
```

### res.write()

- 기본 모듈인 http만으로 가능한 전송함수
- 여러번 보낼 수 있다
- 단 head와 end함수를 직접 지정해야함

### res.end()

- 응답 프로세스를 종료한다

### res.send()

- 다양한 유형의 응답을 전송
- res.write()와 res.end()의 통합방식 : 한번만 사용 가능


### res.redirect()

- 요청의 경로를 재지정

# 파라미터 전송법
## Query string
- req.param()을 이용해 querystring을 통해 요청된 파라미터를 받을 수 있다
```javascript
app.get('/user', function (req, res) {
   var u_name = req.param('name');
   var u_age = req.param('age');

   res.send("User Name : " + u_name + " / User Age : " + u_age);
});
//http://localhost:3000/user?name=kim&age=20'
```
## Path
- req.params를 이용해 파라미터를 받는다
```javascript
app.get('/user/:name/:age', function (req, res) {
   var params = req.params;
   console.log(params);
   
   res.send("User Name : " + params.name + " / User Age : " + params.age);
});
//http://localhost:3000/user/kim/20
```

# 404 응답처리

### 발생 이유

- Express에서 404 응답은 오류로 인해 발생하는 결과가 아니라고 한다
    - 서버와 통신할 수는 있지만 서버가 요청한 바를 찾을 수 없다는 것을 가리키는 HTTP 표준 응답 코드
    - 따라서 오류 핸들러(error-handler) 미들웨어는 이를 파악하지 않음

### 처리법

- 이를 처리하려면 다음과 같이 404 응답을 처리하기 위한 미들웨어 함수를 스택의 가장 아래(다른 모든 함수의 아래)에 추가해야함 (다른 method 및 라우트 호출을 정의한 후 마지막)

```jsx
app.use(function(req, res, next) {
  res.status(404).send('Sorry cant find that!');
})
```

### error-handler 설정법

- error-handler middleware는 다른 미들웨어와 동일한 방식으로 정의할 수 있지만,  4개의 인수 `(err, req, res, next)`시그니처를 갖는다는 점이 다르다

```jsx
app.use(function(err, req, res, next) {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

# Middleware

- 요청(req), 응답(res), 그 다음 middleware 함수에 대한 액세스 권한을 갖는 함수
- 그 다음 middleware 함수는 next라는 이름의 변수로 표시됨(일반적으로)
- 현재 middleware 함수가 req-res 주기를 종료하지 않은 경우 next ( )를 호출해 다음 middleware에 전달해야 한다
- 먼저 로드되는 미들웨어 함수가 먼저 실행

### 기능

- 모든 코드를 실행.
- 요청 및 응답 오브젝트에 대한 변경을 실행.
- 요청-응답 주기를 종료.
- 스택 내의 그 다음 미들웨어를 호출

### 예시

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/745f9ca6-3067-4282-bde3-33ab7c91da4b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220925%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220925T060729Z&X-Amz-Expires=86400&X-Amz-Signature=0ee55b6aced112d1f5891b3355932a4f43024e3445cbbae0742235291f426058&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

### 사용 예시1

- middleware함수를 지정해 app.use( )로 호출

```jsx
import express from "express";
const app = express();

const myLogger = function (req, res, next) {
  console.log('LOGGED');
  next();
};

app.use(myLogger);

app.get('/', function (req, res) {
  res.send('Hello World!');
});

app.listen(3000);
```

- 다음 예시코드는 루트 경로 “/” 로 라우팅하기 전에 `myLogger`라는 middleware함수를 로드하고 있다
    - 루트 경로에 대한 라우팅 이후에 `myLogger`가 로드되면, 루트 경로의 라우트 핸들러가 요청-응답 주기를 종료하므로 요청은 절대로 `myLogger`에 도달하지 못하며 앱은 “LOGGED”를 인쇄하지 않는다
- 앱이 요청을 수신할 때마다, 앱은 “LOGGED”라는 메시지를 터미널에 인쇄
