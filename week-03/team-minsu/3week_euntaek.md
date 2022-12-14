# 3주차 학습내용 정리



# 동적 컨텐츠 작업및 템플릿 엔진 추가

데이터를 js에 저장하여 여러 사용자들로부터 들어오는 요청이

공유되고 있는지 확인할 수 있다.

```jsx
const products = [];
```

새로운 상수로 products 배열을 만든다.

배열 ⇒ 객체 ⇒ 새로운 요소를 받을 수 있음.

shop페이지를 재로딩하면 빈 배열이 나온다.

Add Product 페이지에서 Book을 추가하고 재로딩하면 배열안 book요소가 추가됨.

객체, 배열과 같이 참조유형을 내보내기 하면 다른 파일에서 변경해도 업데이트가 됨 ⇒ 데이터가 공유됨

다른 브라우저에서 로컬 호스트 3000에 접속해도 내용은 같음.

⇒실행중인 노드 서버에 내재된 데이터에서 사용자간에 공유가된다,

하지만 이는 올바른 설정법이 아니다.

⇒ 다른 사용자의 정보가 노출되기 때문

## 템플릿 엔진

⇒HTML과 유사한 템플릿을 인식하고 엔진 종류에 따라 플레이스 홀더나 특정 스니펫을 실제 HTML 콘텐츠로 교체한다.

⇒ Node/Express 앱에 있는 데이터에 대한 목록 항목들이

포함된 순서 없는 목록을 출력할 수 있다.

⇒사용자들은 탬블릿 서버에서 일어나는 일을 볼 수 없고 동적으로 상황에 따라 생성된 html을 볼 수 있다.

=>템플릿 엔진이란, 지정된 템플릿 양식과 데이터가 합쳐져 HTML문서를 출력하는 소프트웨어를 이야기한다. 쉽게 이야기해서, 웹사이트 화면을 어떤 형태로 만들지 도와주는 양식이라고 생각하면 된다.

### 서버 템플릿 엔진, 클라이언트 템플릿 엔진 
=> 여러 양식들중 JSP, Freemarker, 리액트, 뷰와 같은 View 파일이 있다.
모두 지정되어있는 템플릿과 데이터를 이용하여 HTML을 생성하는 템플릿 엔진이지만, 전자는 서버 템플릿 엔진, 후자는 클라이언트 템플릿 엔진이다.

JSP를 비롯한 서버 템플릿 엔진은 서버에서 구동된다.

### 대표적인 템플릿 엔진

1.EJS

2.Pug

3.Handlebars

위 세 모듈은 무료 템플릿 엔진이다.

⇒ 템플릿 생성 + 동적 컨텐츠를 삽입하여 html파일을 얻는다.

1.EJS

```jsx
<p><%= name %></p>
```

일반적인 html의 마크업을 사용하고 작업의 종류에 따라 = 기호를 넣어 사용하기도 한다. 출력을 원하는 통적 콘텐츠를 입력할 수도 있다.

⇒일반 html을 사용하고 단순한js를 사용할 수 있게 하는 플레이스 홀더가 있기에 for루프를 통해 if문 작성가능

2.Pug

```jsx
p #{name}
```

Pug는 다른 구문을 사용하여 실제 html을 사용하지 않고 최소 버전으로 대체하며 #{}구문등을 동적 컨텐츠와 함께 출력한다.

⇒if문들과 목록들도 포함할 수 있고 반복문도 포함될 수 있다.

### 퍼그의 조건문과 반복문
1.조건문
우리가 알고있는 if문과 case문을 활용한다.
```jsx
if flag
  p TRUE입니다.
else
  p FALSE입니다.
case animals
  when 'dog'
    p dog
  when 'cat'
    p cat
  when 'bird'
    p bird
  when 'mouse'
    p mouse
  default
    p So...What is this?
```

2.반복문
each 혹은 for 키워드로 반복문을 사용할 수 있다.
```jsx
<ul>
  <li>dog</li>
  <li>cat</li>
  <li>bird</li>
  <li>mouse</li>
</ul>
ul
  each animals in ['dog', 'cat', 'bird', 'mouse']
    li animals
```

3.Handlebars

```jsx
<p>{{name}}</>
```

Handlebars는 html을 사용하는 대신 동적 컨텐츠의 경우 Ejs와 비슷하게 이중 중괄호를 사용하는 플레이스 홀더가 있다.

⇒html을 사용함과 동시에 제한된 기능의 맞춤형 템플릿언어도 사용하며 if문과 목록등 공통 요소들을 포함한다.

## 퍼그 설치와 구현

템플릿 엔진 3개 설치 ⇒ npm install --save

패키지 pug를 사용하려면 app.js파일의  express.js에게 알려야한다.

### app.set();

```jsx
app.set();
```

app.set을 사용하면 

Express 애플리케이션 전체에 어떤 값이든지 설정할 수 있으며

Express가 이해할 수 없는 키 + 구성 항목도 포함한다.

### app.get();

```jsx
app.get();
```

app.get을 사용하면 app객체에서 읽을 수 있다

⇒데이터 공유 방법

### view 엔진과 views 키

view 엔진

⇒ 

Express에게 특별한 함수를 사용하여 동적 템플릿을 렌더링 하기위해 이 엔진을 사용해달라고 알리고 view는 express에게 이러한 동적 view를 어디에서 찾을 수 있는지 알리는 기능이 존재한다.

### app.set();

```jsx
app.set();
```

app.set();을 사용해 여기 view를 설정하여 view engine을 string, pug로 설정하는데 여기에는 아무것도 입력할 수 없다 여기에 pug를 사용하는 이유는 pug템플릿 엔진을 설치했고 이 엔진은 내장된 익스프레스 자원과 함께 전달되고 익스프레스에 자신을 자동등록 하기 때문이다.

## Handlebars 사용하기

Handlebars는 pug와 다르게 app.set으로 익스프레스에게 엔진을 알리지 않는다.

Handlebars는 익스트레스에 자동적으로 설치되는 패키지가 아니다.

⇒불어오기를 해야함,

```jsx
import express-handlebars from "express-handlebars";
```

불러온후 위 엔진이 사용가능하다고 알려야됨.

```jsx
app.engine('handlebars' , express.Hbs);
```

위 코드를 통해 새로운 템플잇 엔진을 등록함. ⇒'handlebars'와 같이 이름을 붙여주고 , 뒤에 express.Hbs를 작성하여 어떠한 툴을 사용할지 알린다.

## EJS 사용하기

ejs는  pug와 같이 즉시 지원이 되는 템플릿 엔진이다.

Handlebars에서 사용했던 임포트 문과 엔진을 삭제하고

pug와 동일하게

```jsx
app.set('view engine', 'ejs');
```

다음과 같이 ejs로 설정해주면 된다.