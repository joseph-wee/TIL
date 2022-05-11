# react 실시간강의 - 220511

## React 프로젝트 시작하기
- CRA(create-react-app)이란?

> react프로젝트를 위한 boilerplate

### CREA로 react 프로젝트 생성하기
- `npx create-react-app my-app --template typescript` 으로 react 프로젝트를 생성할 수 있다. (typescript로 만든것 다른걸로 만들려면 빼거나 다른걸로 하면 될 듯 싶다.)

### CRA의 package.json 살펴보기
- 프로젝트를 열어볼 때 package.json 을 먼저 보는걸 추천
- 기본적으로 dependency들이 숨겨져있음
- eject scripts를 통해 webpack, babel등 dependency들 확인이 가능하다.
- 하지만 많은 dependency가 숨겨져있다.
- start/build scripts 또한 eject통해 확인 가능.

### React Element와 Component
- React Element = render하기 위한 정보를 담아둔 객체
- React Component = React Element를 return 하는 함수
- JSX = React Element를 생성하기 위해 사용하는 문법적 sugar

### React Component에서의 props
- Props=Component 라는 함수를 호출할 때 넘기는 인자
- React에서 Props 항상 객체
- 컴포넌트 합성

childeren 의 자료형은 ReactNode 이다.