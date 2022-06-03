# 6주차 리엑트기초 Ch 02.07 ~ Ch03.19, 리엑트 라이브러리 Ch 01 ~ Ch 02, Ch04, Ch05.01~07, Ch07.01~06

## State
- 컴포넌트 내의 상태: props를 변경하는것이 아닌 state를 통해서 자신의 출력값을 변경

## 컴포넌트 생명주기

## 이벤트
리엑트에서는 preventDefault를 명시적으로 호출해야 기본동작을 방지할 수 있다.
버블링이란 어떤 컴포넌트나 엘리먼트를 클릭하면 그 부모로 이 애들을 계속 전파하는것
캡쳐링이란 내 자식들 중에 누가 클릭했는지 확인하기 위한 체크과정
캡처링 후에 버블링이 일어난다.



## 조건부렌더링
- if(condition){return A} else {return B} 형태
- &&: condtion && A, flasy를 주의 해야한다. 명확하게 false면 렌더링이 안되는데 falsy 값이 들어가면 렌더링이 된다.
- 삼항연산자 이용하거나
- 아예 그리고 싶지 않을 때는 return null

## Form
- Controlled Component: input의 value를 state로 관리
- 다중입력: event.target.name
- Uncontrolled Component: form element 자체의 내부 상태 활용
- defaultValue, ref: 기본값 value 확인

## Hooks
- Hopks 등장: Class의 단점 보완, 재사용성 강화
- Hook 사용 규칙: 최상위에 두어야하며 조건문을 통해서 hook자체를 사용안사용하게 해서는 안되며 함수형 컴포넌트, custom Hook에서 사용가능
- Class state: 훅을 먼저 배웠기에 고민할 필요가 없다.
- useEffect: 데이터 fetch, 구독, Dom수정
- clean up: 구독과 구독해지를 한공간에서 할 수 있다.
- dependenct array: 필요한 변경시에만 effect 실행
- custom hook: 컴포넌트들에 반복되는 hooks 묶기
- 다양한 hooks: 필요한 타이밍에 참고해서 사용

## Composition
- Composition : 컴포넌트에 컴포넌트 담기
- 담는방법: Childeren, Custom
- typeof: type check
- 확장성: 다양한 상황을 품을 수 있도록

## HOC
- 함수를 받아서 함수를 리턴, 컴포넌트를 받아서 컴포넌트를 리턴

## Memoization
- React.memo: HOC, Props 비교하여 메모
- Profiler: 리엑트 성능 분석 도구
- callback: useCallback
- value: useMemo

## Context
- 컴포넌트 트리 제약: props drilling의 한계 해소
- 재사용성: Context를 사용하면 재사용하기 어려움
- API: createContext / Provider / Consumer
- useContext: Consumer가 대체

## Portals
- createPortal: 부모 컴포넌트 DOM트리로부터 벗어나기
- 이벤트 Portal에 있더라도 Event는 트리로 전파

## Render Props
- render props: 무엇을 렌더링할 지 알려주는 함수
- render일 필요: 없음, children도 되고 뭐든 됨
- PureComponent: props,state비교하여 성능 최적화

## PropTypes
- 개발모드에서만 동작: 유효하지 않은 prop에 대한 경고
- custom: RegExp등으로 사용자 정의 가능
- children 제한: 원래 제약없던 갯수 제약 가능

## Reconciliation
- 루트부터 비교: 무엇을 렌더링할 지 알려주는 함수
- 트리를 파괴: 부모가 바뀌었다면 트리를 버린다.
- Keys: 자식 재귀 처리시 효율성 확보
- Virtual DOM: 실제 DOM과 동기화 할 가상 표현
- 재조정: 실제 DOM과 Virtual DOM의 동기화
- React Fiber: 스택 reconciler 대체한 재조정 엔진

## 라이브러리란
- 라이브러리: 공구, 도구
- 라이브러리 도입 과정: 필요 -> 검색 -> 사용법 파악-> 적용
- 사용법을 익히기보다는 찾고, 적용하는 과정을 익히자

## Moment
- 타임존: moment, timezone
- Format, 비교: 원하는 스타일로 표기 가능
- 오래됨: Mutable, Tree shaking X

## Day.js
- 타임존: plugin, timezone plugin, utc
- Format, 비교: 원하는 스타일로 표기 가능
- 가벼움: Tree shaking X

## date-fns
- 타임존: date-fns-tz
- Format, 비교: 원하는 스타일로 표기 가능
- 포괄적임: immutable, tree shaking 까지
- 함수별 import: 가능, ex. addWeeks


## styled-components
- CSS in JS: CSS의 문제점을 해소
- 해결책: 스타일을 style 태그로 분리
- 사용법(Template literals): styled.{element}``
- styled(스타일드컴포넌트): 상속
- &: 가상 엘리먼트, 가상 선택자
- Global Style: 전역 스타일
- attrs: props addtion
- keyframes, ThemeProvider: animation, theme

## emotion
- react에 특화: @emotion/react
- css props: jsx를 대체함
- styled components: styled-component + @
- compostion: css안에서 css사용
- 기능: Fallbacks, &, Global, keyframes
- styled-components: 서로 점점 유사해짐
- trend: emotion이 우세한 듯
- 사이즈, 속도: emotion이 우세한듯

## sass
- 전처리기: css의 확장
- Sass, Scss: 보다 css와 유사한 scss
- 사용: variables, modules, mixin, extend
- syntax: 언어처럼 자체 syntax가 있음
- interpolation: #{} 값을 주입(마치 ${})
- values / functions: 프로그래밍 언어스러움

## msw
- Mocking: 모의 데이터 활용
- Browser: Service worker 활용
- REST API, GraphQL: 모두 모킹이 가능
- mock: handler, brower 만 있어도 동작
- public: npx msw init<PUBLICK_PATH>
- 기타 커스텀: query, patching, error

## Redux
- 전역상태관리: vs 지역상태관리
- 단 방향 데이터(상태)흐름: Flux
- 구성요소: store, reducer, action, selector
- RTK: redux 라이브러리들 조합
- 라이브러리들: immer, saga, thunk, reselect
- redux dev tools: chrome extension
- hooks: useSelector, useDispatch
- API 통신: 비동기 작업(RTK-Query)
- Redux-Thunk: Action으로 API 요청,결과 Store에 반영

## Mobx
- Simple: No Boilerplate
- Action: Derivative를 바꾸는 유일한 수단
- Reactive Programing: Observable, Observer
- with React: re-render issue (small component)
- makeAutoObservable: makeObservable을 보다 쉽게
- actions: runInAction, flow
- Computed: getter pure
- reaction: side effect
- reactve: observable 인 것이 바뀔 때


## GraphQL
- 쿼리: 요청, 결과동일, 주석, 작업(타입,이름)
- 쿼리: 필드 객체 참조(다중콜 x), 인자, 별칭
- Fragment: 반복되는 필드셋, 변수 전달 가능
- 변수, 지시어: 동적쿼리 방법/ @include @skip
- 뮤테이션: 데이터의 수정을 가하는 방법
- Apollo graphQL: 다양한 기능이 추가된 라이브러리
- 뮤테이션 다중필드: 순차 실행(쿼리르 병렬)
- 인라인 프래그먼트: interface, union 일때 사용
- 타입 시스템: 객체 타입과 필드
- 특별한 타입: 쿼리 타입, 뮤테이션 타입
- 스칼라 타입: 구체적 데이터
- 기타: 인터페이스, 유니온, 인풋


***
- clear, useEffect, this, && 연산자, bind
- submit의 디폴트 액션은 페이지를 넘기는것

