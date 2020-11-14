# Nomflix

Learning React and Es6 by building a Movie Discovery App.

## Screens

- [ ] Home
- [ ] TV Shows
- [ ] Search
- [ ] Detail

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
