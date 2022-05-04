# React 특강
- react.app 개발하려면 깔아야 할 것들이 꽤 있다.
    - react, react-dom, testing라이브러리, webpack...
    - 하지만 create-react-app으로 한 번에 필요한 것들을 다 설치가 가능해졌다.
- webpack -- 2021년 3월기준
- vite -- 요즘에 쓰는 것
- npx create-react-app my-app
- 명령어 이용하려면 루트 디렉토리 my-app 으로 이동해야함.
- 컴포넌트란
  - 개발자가 만든 태그라고 볼 수 있다
  - 컴포넌트 이름의 시작을 대문자로 만들어야한다.
  - 리턴구문 안에 태그는 하나만 써야한다.
    - 여러개를 쓰고싶다면 태그안에 담아서 여러개를 쓸 수 있다.
    ```js
    return(
      <div>
      <p>asdf</p>
      <p>asdf</p>
      </div>
    )
    ```
    - 여러개를 쓰기위해 일부러 감싸는 태그를 만들어야 한다면 <></>라는 fragment를 이용할 수 있다.
    ```js
    return(
      <>
      <p>asdf</p>
      <p>asdf</p>
      </>
    )
    ```
- 2. js
- js파일에서 리턴안에 html내용넣을 때 태그에 클래스 이름을 주고싶으면 class=""가 아닌 className=""을 써야한다.


- 리액트가 화면이 바뀔 때 바뀌는 부분은 바꿔주고 안바뀌는 부분은 그대로 둔다.
- 네이버 vibe사이트를 보면 옆에있는 메뉴를 클릭하면 새로고침이 일어나지않으면서 바로 화면이 바뀐다.
  
```js
function useState()


// 리턴은 소괄호로 열어주어야 한다.
    // html관련 내용을 넣는곳

      //javascript내용을 넣는곳
  //camelCase를 지키자.
  // 배열로 리턴하는 함수의 값을 배열로 받을 수 있다.
  // state: 문자, 숫자, 배열, 오브젝트, 기타 등등
  //es6+문법

  // const 숫자늘리기 = () => {
  //   setTarget(Target+1);
  // }

        // 1. List 배열을 반복문을 통해 보여준다.
      // 2. 버튼을 하나 만들고
      // 3. 그 버튼을 클릭 Target의 값을 List에다가 집어넣을것
      // 4. 집어넣고 Target의 값을 1 증가시킨다.


      import React, { useState } from "react"

function App(){

  const [Target, setTarget] = useState(false);
  const 바꾸기 = () => {
    setTarget(!Target);
  }


  return(
    <div style={{margin: "20px"}}>
      {
        Target ?
        <p>타겟이 트루임!</p> :
        <p>타겟이 펄스임</p> 
      }
      
      <button onClick={바꾸기}>타겟바꾸기</button>
    </div>
  )
}

export default App;




import React, { useState } from 'react'


function App() {


  const [List, setList] = useState([0]);
  const [Target, setTarget] = useState(1);

  const ListFunction = () => {
    let temp = [...List];
    temp.push(Target);

    setList([...temp]);
    setTarget(Target+1);
  }
  return (  
    <div>
      <p>리스트: {List}</p>
      <p>타겟 : {Target}</p>
      <br/>
      <button onClick={ListFunction}>누르면 타겟의 값이 List에 들어감.</button>
    </div>
  )
}

export default App;
```
- 암묵적으로 {} 안에는 js구문 ()안에는 html구문
- react style guide라고 규칙이 있는데 
