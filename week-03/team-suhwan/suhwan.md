### 요청 간의 데이터 공유

객체나 배열 같은 참조유형을 내보낼 수 있다.

**admin.js**

```jsx
const products = [];
//
//
export { router, products }; //다른 파일에서 import하여 접근
```

**app.js**

```jsx
import { products } from "admin.js";
```

### 템플릿 엔진

- HTML페이지에 동적 컨텐츠를 넣을 수 있게 한다.
- 서버에서 데이터를 미리 정의된 템플릿에 넣어 html을 렌더링해 클라이언트에 전달

- HTML의 기본 구조, 스타일, javascript등 기본적인 코드들이 해당
- 템플릿 엔진을 통해 우리가 Node/Express 에서 작성한 컨텐츠들이 HTML 콘텐츠로 변환되어 HTML파일이 된다.

**서버 사이드 렌더링 vs 클라이언트 사이드 렌더링**

- 서버 사이드 렌더링: 서버에서 데이터를 렌더링해 완전한 HTML을 만들어 전달
- 클라이언트 사이드 렌더링: 서버로부터 제공 받은 데이터를 클라이언트에서 렌더링해 HTML 화면을 동적으로 만든다.

- **템플릿 엔진을 사용하는 이유?**
  - 장점
    - 코드를 간단하게 줄일 수 있다. ex)리스트 출력
    - 속도가 빠르다.(클라이언트에서 데이터를 랜더링할 필요가 없음)
  - 단점
    - 또 다른 문법(사용 법)을 익혀야 한다.
    - 동적이면서 복잡한 화면을 만들기 어렵다.

**설치 및 구현**

- express 앱을 저장한 변수 ex)app 에서 `set()` 사용
  - `set()` 을 통해 Express 애플리케이션 전체에 어떤 값이든 설정 가능
  - `get()` 을 통해 값을 가져올 수 있음

```jsx
app.set("view engine", "pug");
```

- 모든 템플릿 엔진이 이러한 형태로 사용할 수 있는 것은 아니다.(pug는 express에 스스로를 자동으로 등록하기 때문에 사용 가능)
- view를 찾는 경로에 대한 기본값은 메인디렉토리 + /views

**템플릿 엔진 렌더링**

- `res.sendFile()` → `res.render()`
- `res.render()` 는 기본 템플릿 엔진을 통해 렌더링함

**동적 컨텐츠 출력**

- express의 데이터를 템플릿 엔진에서 사용할 수 있도록 `render()`함수에 자바스크립트 객체 형태로 전달
  - `res.render(”a”, {prods: poducts})` : 템플릿에서 prods로 products에 접근 가능
