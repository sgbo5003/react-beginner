# Nomflix

Learning React and Es6 by building a Movie Discovery App.

## Screens

- [ ] Home
- [ ] TV Shows
- [ ] Search
- [ ] Detail

## API Verbs

- [x] Now playing (TV, Movie)
- [x] Upcoming (Movie)
- [x] Top Rated (TV)
- [x] Popular (TV, X)
- [x] Airing Today (TV)
- [x] TV Show Detail
- [x] Movie Detail
- [x] Search (Movie, TV)

<br>

# 11/14 일자 공부내용

## 2-2 React Router part Two

### **HashRouter 와 BrowserRouter**

**HashRouter**

**url** : localhost:3000/#/

url을 이쁘게 보여주지는 않지만 **간단**하다.

내 페이지의 **Hash** 를 사용

**정적인 페이지**에 적합

### **둘의 기능은 같다.**

**BrowserRouter** : 일반적인 페이지처럼 작동한다

**url** : localhost:3000/

**HTML history API** 를 사용

**동적인 페이지**에 적합

**Composition** : **두 개 이상**의 Route를 랜더링하는 방식 (동시에)

**Switch** : 한 번에 오직 **하나**의 `<Route>`만 Render하게 해준다.
`<Switch>`내부에 `<Route>`들을 넣으면 요청에 의해 매칭되는 `<Route>`들이 다수 있을 때에 **제일 처음 매칭되는 Route만 선별**하여 실행하기 때문에 충돌 오류를 방지 할 수 있다.

**exact** : **exact** 또는 **exact = {true}** 는 /  가 포함된 url이 아니라 정확히 / 로 들어왔을 때만 해당 컴포넌트를 그려주게 해주는 것이다.

**Redirect** : 요청 경로를 다른 경로로 리다이렉션

## 3-0 CSS in React part One

컴포넌트를 이용해서 어플리케이션의 부분 부분을 **캡슐화** 하고싶기때문에 파일들을 **분리**

## 3-1 CSS in React part Two

css파일을 그냥 만들어서 쓰면 global 하기 때문에 다른 className과 **중복**되는 것을 신경 써야된다.

**해결책**

**CSS 모듈** : 우리의 className을 **임의화**(randomize)해서 css global이 아닌 local이 되게 하는 것

**<방법>**

1. css의 이름을 00.module.css 이런식으로 바꾼다
2. import 해줄 때 자바스크립트처럼 import styles from "./00.module.css"; 이렇게 해준다.
3. className을 넣어줄 때도 마찬가지로 `<ul className = {styles.navList}>` 이렇게 해준다.

**장점**

1. className이 랜덤으로 생성되서 중복되는 이름 사용가능
2. CSS 클래스가 중첩되는 것을 완벽히 방지 가능

**단점**

1. className을 기억해야 한다.
2. className에 nav-list 처럼  중간에 작대기를 못넣어 준다.

**쓰기 유용한 상황**

- 레거시 프로젝트에 리액트를 도입할 때 (기존 프로젝트에 있던 CSS 클래스와 이름이 중복되어도 스타일이 꼬이지 않게 해줍니다.)
- CSS 클래스를 중복되지 않게 작성하기 위하여 CSS 클래스 네이밍 규칙을 만들기 귀찮을 때

## 3-2 CSS in React part Three

**Link** : 해당 페이지가 내 어플리케이션에 있으면 그 곳으로 브라우져한 방식으로 가지 않고 JavaScript의 방식으로 가게 해준다.

**SASS** : CSS전처리기(CSS pre-processor)라 불리는 **SASS**(**Syntactically Awesome StyleSheet**)는 CSS의 단점을 보완한 CSS의 확장형이다.

### **styled-components**

**사용법**

1. npm add styled-components // 설치
2. import styled from "styled-components"; // import
3. const Header = styled.header``; // 이런 식으로 정의
4. html 태그를 위에서 정의한 변수 이름으로 바꿔준다.

ex)
**Header.js**

```
import React from "react";
import { Link } from "react-router-dom";
import styled from "styled-components";
const Header = styled.header``;
const List = styled.ul`
  display: flex;
  &:hover {
    background-color: blue;
  }
`;
const Item = styled.li``;
const SLink = styled(Link)``;
export default () => (
  <Header>
    <List>
      <Item>
        <SLink to="/">Movies</SLink>
      </Item>
      <Item>
        <SLink to="/tv">TV</SLink>
      </Item>
      <Item>
        <SLink to="/search">Search</SLink>
      </Item>
    </List>
  </Header>
);
```

## 3-3 GlobalStyles and Header

현재 styled-components 가 local 하기 때문에 global 하게 스타일

**global 스타일을 하는 이유** : 해당 사이트의 폰트를 설정하거나 SC를 설치하거나 하고싶어서

npm add styled-reset

**styled-reset** : SC를 이용해서 css를 초기화해서 0의 상태에서 시작하게 한다.
예를들어 **reset.css, default.css** 와 비슷한 개념?

ex)**GlobalStyles.js**

```
import { createGlobalStyle } from "styled-components";
import reset from "styled-reset";
const globalStyles = createGlobalStyle`
    ${reset};
    a{
        text-decoration:none;
        color:inherit;
    }
    *{
        box-sizing:border-box;
    }
    body{
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
        font-size: 12px;
        background-color: rgba(20, 20,20, 1);
        color:white;
        padding-top:50px;
    }
`;
export default globalStyles;
```

ex)**App.js**

```
import React, { Component } from "react";
import Router from "../Components/Router";
import GlobalStyles from "../Components/GlobalStyles";
class App extends Component {
  render() {
    return (
      <>
        <Router />
        <GlobalStyles />
      </>
    );
  }
}
export default App;
```

추가로
react에서 styled-components 를 할 때 style 자동완성이 안되서 불편했다.

해결방법 : extension에서 **vscode-styled-components Extension** 설치

<br>

# 11/15 일자 공부내용

## 3-4 Location Aware Header

SC(styled-components)에서는 SC에 props를 줄 수 있다.

```
 border-bottom: 5px solid
    ${(props) => (props.current ? "#3498db" : "transparent")};
```

### **withRouter**

**withRouter** : 다른 컴포넌트를 감싸는 컴포넌트, Router에 어떠한 정보를 준다.

어떤 컴포넌트와도 **연결**할 수 있다.

withRouter는 주로 **history에 접근**하여 컴포넌트에서 라우터를 **조작**하는 데 사용

라우트가 아닌 컴포넌트에서 라우터에서 사용하는 객체 - **location, match, history 를 사용하려면**, withRouter를 사용해야 한다.

withRouter 고차원 컴포넌트를 통해 history 객체의 속성과 가장 가까운 match 액세스 할 수 있다.

withRouter는 render props : { match, location, history } 와 같은 props로써 경로가 변경 될 때마다 해당 구성 요소를 다시 렌더링한다.

## 4-0 Networking Introduction to The Movie DB API

movie app API KEY

10923b261ba94d897ac6b81148314a3f

## 4-1 Sexy Networking with Axios Instances

axios를 이용

## 4-2 API Verbs part One

가져올 API들 정리

```
export const moviesApi = {
  nowPlaying: () => api.get("movie/now_playing"),
  upcoming: () => api.get("movie/upcoming"),
  popular: () => api.get("movie/popular"),
};
export const tvApi = {
  topRated: () => api.get("tv/top_rated"),
  popular: () => api.get("tv/popular"),
  airingToday: () => api.get("tv/airing_today"),
};
```

## 4-3 API Verbs part Two

```
import axios from "axios";
const api = axios.create({
  baseURL: "https://api.themoviedb.org/3/",
  params: {
    api_key: "10923b261ba94d897ac6b81148314a3f",
    language: "en-US",
  },
});
export const moviesApi = {
  nowPlaying: () => api.get("movie/now_playing"),
  upcoming: () => api.get("movie/upcoming"),
  popular: () => api.get("movie/popular"),
  movieDetail: (id) =>
    api.get(`movie/${id}`, {
      params: {
        append_to_response: "videos",
      },
    }),
  search: (term) =>
    api.get("search/movie", {
      params: {
        query: encodeURIComponent(term),
      },
    }),
};
export const tvApi = {
  topRated: () => api.get("tv/top_rated"),
  popular: () => api.get("tv/popular"),
  airingToday: () => api.get("tv/airing_today"),
  showDetail: (id) =>
    api.get(`tv/${id}`, {
      params: {
        append_to_response: "videos",
      },
    }),
  search: (term) =>
    api.get("search/tv", {
      params: {
        query: encodeURIComponent(term),
      },
    }),
};
```

<br>

# 11/16일 공부내용

## 5-0 Container Presenter Pattern part One

리액트는 Component 단위로 개발한다.
근데 그거 말고는 딱히 정해진 양식이 없다.
이벤트 제어도 자유 (권장하는 방식이 있긴 있음) css 스타일링도 자유다.

**Container Presenter Pattern(리엑트 컴포넌트 코딩 패턴)**

데이터처리와 데이터출력을 분리 (logic 과 presenter를 분리)

**Container** : API Request, Exception Error, setState... ETC...

**Presenter** : only Props, UI, no logic

이런 구조로 만드는 것이 Container + presenter 패턴

**<핵심>**

**Container** : 데이터 로직 처리~~~ 이것저것 해서 props로 넘긴다.

**Presenter** : 그걸 props로 받아서 보여주기만 한다

## 5-1 Container Presenter Pattern part Two

각각 폴더에 Container.js, Presenter.js를 만들어 분리

## 5-2 Home Container

**async, await** : 내가 무언가를 끝낼 때 까지 기다리게 하고 싶을 때 사용

**객체 비구조화 할당** 사용

<br>

# 11/17일 공부내용

## 5-3 TV Container

**async**라는 함수안에서만 **await**를 쓸 수 있다.

## 5-4 Search Container

## 5-5 Detail Container part One

## 5-6 Detail Container part Two

**includes()함수** : 문자열이 특정 문자열을 **포함**하는지 확인하는 메서드

## 5-7 Destructuring assignment with let

## 6-0 Presenter Structure

Presenter들 구조화

<br>

# 11/18일 공부내용   

## 6-1 HomePresenter and Section Components

Movie 화면에 Now Playing , upComing Movies, Popular Movies 띄우기, style 입히기

## 6-2 TVPresenter and Loader Components

**aria-label** : 시각장애인들을 위해

```
<span role="img" aria-label="Loading">
      ..Loading
    </span>
```

<br>

# 11/19일 공부내용

## 6-3 SearchPresenter Component

**all : unset**
기본 스타일을 한번에 **초기화** 해준다.

```
 all: unset;
```

## 6-4 Message Component

Message.js Coding

## 6-5 Poster Component part One

Poster.js Coding

## 6-6 Rendering Poster Component

**substring(0, ~)**
: ~까지 문자열을 잘라준다.

## 6-7 Poster Component part Two

Poster Component Styling

<br>

# 11/23일 공부내용

## 6-8 Detail Container part One

Detail 페이지 배경사진, 포스터 사진 styling, coding

## 6-9 Detail Container part Two

Detail 페이지 제목, 연도, 상영시간, 장르, 상세내용 styling, coding

**span**은 **margin**을 가지지 않는다.

## 6-10 React Helmet

**react-helmet 설치**

> npm add react-helmet

**react-helmet**

웹 문서의 **헤더 값을 변경**할 때 사용하는 **리액트 컴포넌트**이다

react-helmet을 사용해 title 바꾸기 각 화면마다 title 다르게 보이게 하기

**Fragments** (<>)
리액트에서는 하나의 컴포넌트가 여러 개의 엘리먼트들을 반환한다.
리액트를 사용하기 위한 문법인 JSX 를 쓸 때, return 문 안에는 반드시 **하나**의 최상위 태그가 있어야 한다. 이는 리액트가 **하나**의 컴포넌트만을 리턴할 수 있기 때문이다.

하지만, **Fragments**는 DOM에 별도의 노드를 추가하지 않고 **여러 자식**을 **그룹화** 할 수 있다.

<br>

# 11/24일 공부내용

## 6-11 Code Challenges

detail 페이지에서 나 스스로 몇 가지를 더 추가

추가한 것 : 링크를 만들어 클릭하면 영화를 볼 수 있는 사이트로 이동( imdb 사이트, 바로 그 영화가 뜨게 했다) , 제작한 나라 표시

## 7-0 Deploy to Github Pages

**깃헙 페이지 생성**

> https://sgbo5003.github.io/react-beginner

안될때는 주소 뒤에 /#

## 7-1 Deploying to Netlify

Github Pages 이랑 비슷한 Netlify가 있다. (github와 연동)
