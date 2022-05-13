# Ch 01. React 맛보기 04~14

## 멀티 Element 생성하기
- fragment를 이용해서 그 안에서 html의 문법을 그대로 사용 할 수 있다.
```jsx
<React.Fragment>
  <h1>안녕</h1>
  <h2>이런식</h2>
</React.Fragment>
```
- 아니면 `<React.Fragment>` 대신에 `<>`, `</>` 를 사용도 할 수 있다.

## Element 찍어내기
- funciton: 재사용 가능한 Element
- custom element = Upper case로 함수 이름으로 사용해야 에러가 나지 않는다.
- children 제한이 없다.

## JS와 JSX 섞어쓰기
- interpolation : js와 jsx를 섞어쓰는것을 말한다.

## 리액트의 리랜더링 알아보기
- 바닐라 js: 변경으로 인해 element를 다시 그림
- react: 변경된 부분만 다시 그림
- 리액트 엘리먼트는 불변객체이다.
- 우리는 ReactDOM.render(element, rootElement); 로 전달할 뿐 변경 판단 및 반영은 리엑트가 알아서 한다.
- 엘리먼트 타입이 바뀌면 이전 엘리번트는 버리고 새로 그린다.
- 엘리먼트 타입이 같다면 key를 먼저 비교하고 props를 비교해서 변경사항을 반영한다.
- 정리하자면
  - 리엑트 엘리먼트: 불변객체
  - 변경사항 반영: 리엑트에게 일임
  - 리엑트의 비교: Reconciliation
  - virtual dom: 비교시 활용

## 이벤트 핸들러 써보기
- 바닐라 js: on{event} / addEventListener
- React: on{Evnet}
- 위를 보면 알겠지만 리엑트에서는 카멜케이스를 꼭 써야한다.
- Object.assingn: 객체 내용 복사- 바뀐부분이 있으면 덮어씌움 안바뀌면 그대로 유지
- 전역 변수 변경을 위해서 ReactDom.render을 계속 해야 한다.

## 컴포넌트 상태 다루기
- DOM: 논리트리
- 컴포넌트: 엘리먼트의 집합
- 엘리먼트: 요소
- useState: 상태갑사을 관리해주는 훅

## 컴포넌트 사이드 이펙트 다루기
- 사이드 이펙트: 부수효과
- useState: lazy initialize
- useEffect: dependency array

