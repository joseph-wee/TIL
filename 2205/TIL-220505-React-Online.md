# React 맛보기
### 리엑트란
- 라이브러리는 개발편의를 위한 도구의 모음
- 프레임워크는 기반 구조까지 잡혀있다.
- 라이브러리는 공구 프레임워크는 공장에 비유할 수 있다.
- 리엑트는 공식 홈페이지를 가보면 '라이브러리'라고 소개를 하고 있다. 즉, 그만큼 자유도가 높다는 뜻이다.
### 생태계
- 관심도, 실제사용빈도, 사용자수가 높다.
- 그래서 관련 라이브러리가 많고 문제해결할 방법을 찾기가 쉽고 나와 같은 고민을 한 사람들이 많고 실무에서 사용할 확률이 높다.
- tip: webapalyzer를 크롬 확장도구를 쓰면 특정홈페이지가 언어,라이브러리 등 무엇을 사용하고 있는지 알 수 있다.

## DOM다루기 Element 생성하기
- CodeSandBox: https://codesandbox.io/ 를 이용해서 여러가지 테스트를 할 것
- CDN: Content Delivery Network
  - 웹에서 사용되는 다양한 컨텐츠(리소스)를 저장하여 제공하는 시스템
- React, React-dom : element 생성 , appendChild

## JSX와 Babel, JSX다루기
- JSX란 문자도 html도 아닌 javascript의 확장 문법이다.
- javascript컴파일러인 babel이 필요하다. https://babeljs.io/에서 테스트할 수 있다.
- js에서 변수를 선언해서 jsx에서 다룰 수 있다.

```jsx
<!DOCTYPE html>
<html lang="en">
  <body>
    <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js."></script>

    <div id="root"></div>
    <script type="text/babel">
      const rootElement = document.getElementById("root");

      const text = "Hello,world";
      const element = <h1 className="title">Hello, world!</h1>;
      ReactDOM.render(element, rootElement);
    </script>
  </body>
</html>
```