# JavaScriptLevelUp 온라인 강의

# JS 데이터

## 문자

### String
- `string` 전역 객체는 문자열의 생성자이다.
- `new string()` 를 통해 문자열을 생성 할 수 있다.
### `String.prtotype.indexOf()`
- 호출한 `String`객체에서 주어진 값과 일치하는 첫 번째 인덱스를 반환한다. 일치하는 값이 없으면 -1을 반환한다.
```javascript
const result = 'Hello world!'.indexOf('world');
console.log(result);  // 6출력
const result = 'Hello world!'.indexOf('joseph');
console.log(result);  // -1출력
```

```javascript
vondy dyt = '0123'
console.log(str.length) //4출력
console.log('012 3'.lenth)  //5출력
```
### `String.prototype.slice()`
- 문자열의 일부를 추출하면서 새로운 문자열을 반환한다.
- `str.slice(beginIndex, endIndex)`
- beginIndex: 추출시작점
- endIndex: 추출종료점 인덱스로 그 직전까지 추출한다.
```javascript
const str = 'Hello world!';
console.log(str.slice(6,11)); //world 출력
console.log(str.replace('world', 'joseph')); // world를 joseph으로 대체해서 Hello joseph 출력
console.log(str.replace(' world', '')); // Hello 출력
```
```javascript
const str = 'thesecon@gamil.com';
console.log(str.match(/.+(?=@)/)[0])  //thesecon 출력
/* 정규표현식을 통해 thesecon만 추출*/
```
```javascript
const str = '     Hello World   ';
console.log(str.trim());  // Hello World 출력
//trim(): 앞뒤의 공백 제거
```
## 숫자와 수학
- `parseInt` : 정수를 반환 `parseFloat`: 소수를 반환
- `toFixed()` : 소수점 아래를 버리고 문자열 반환
```javascript
const pi = 3.141592
console.log(pi) // 3.141592출력
const str = pi.toFixed(2) // 3.14문자열 반환
console.log(str)  // 3.14출력, 하지만 숫자가 아닌 문자열임!
const integer = parseInt(str) //str의 정수를 반환
const float = parseFloat(str) //str의 소수형태로 반환
console.log(integer)  //3출력
console.log(float)  //3.14출력
```

### Math
- 수학적인 상수와 함수를 위한 속성과 메소드를 가진 내장 객체이다. 함수 객체가 아니다.

### Math.abs()
- 주어진 숫자의 절댓값을 반환한다.

### Math.min()
- 숫자들 중 최소값을 반환한다.

### Math.max()
- 숫자들 중 최대값을 반환한다.

### Math.ceil()
- 숫자를 올림한다.

### Math.floor()
- 숫자를 내림한다.

### Math.round()
- 숫자를 반올림한다.

### Math.random()
- 무작위 숫자를 반환한다.

## 배열

### .lenth
- 배열의 길이 반환

### .concat()
- 배열들을 합치는데 원본 데이터들은 수정되지 않는다.


### .foreach()
- 붙어있는 메소드의 배열의 크기만큼 반복해서 콜백함수를 실행한다.
```javascript
fruits.forEach(function (fruit, index, array){
  console.log(fruit, index, array)  //array는 잘 안쓰이며 index 는 i로 간소화에서 쓴다. 
})
```
### .map()
- 붙어있는 메소드의 배열의 크기만큼 반복해서 콜백함수에서 실행된 것의 결과를 반환한다.
```javascript
const b = fruits.map(function (fruit, index){
  return{
    id: index,
    name: fruit
  }
})
```

### .filter()
- 필터링된 값을 반환한다. 원본 데이터는 훼손되지 않는다.
```javascript
const b = numbers.filter(number => {
  return number < 3
})
console.log(b)  // number < 3 의 조건에 충족되는 값만 출력된다.
```

### .find()
- 주어진 판별 함수를 만족하는 첫번째 요소의 값을 반환한다. 없다면 undefined를 반환한다.

### .findIndex()
- 주어진 판별 함수를 만족하는 첫번째 요소의 index를 반환한다. 없다면 undefined를 반환한다.

### .includes()
- 값이 포함되어 있다면 true 아니면 false를 반환한다.

### .push()
- 배열의 가장 뒤쪽에 값을 삽입한다. 원본 데이터에 영향을 미친다.

```javascript
numbers.push(5) // 배열의 맨뒤에 5를 삽입
```

### .unshift()
- 배열의 가장 앞쪽에 값을 삽입한다. 원본 데이터에 영향을 미친다.
```javascript
numbers.unshift(5)  // 배열의 맨 앞에 5를 삽입
```

### .reverse()
- 배열의 순서를 반대로 바꾼다. 원본 데이터에 영향을 미친다.
```javascript
numbers.reverse() // 원래 배열이 [1,2,3,4] 였다면 [4,3,2,1]로 바꾼다
```

### .splice
- .splice(index, n, x)이면 배열의 index부터 n개만큼 값을 지운다. 그 자리에 x값을 삽입한다.
- n에는 0을 주어서 특정 자리에 x만 삽입하는 형태로도 사용가능하다.
- x는 생략을 해서 값을 지우는 형태로만도 사용가능하다.
```javascript
numbers.splice(2,1) // 배열[2] 부터 한개의 값을 지운다.
numbers.splice(2,1,5) // 배열[2]의 값을 1개만큼 지우고 그 위치에 5를 삽입한다.
```
## 객체

### Object.assign()
- 열거할 수 있는 하나 이상의 출처 객체로부터 대상 객체로 속성을 복사할 때 사용한다. 원본 데이터에 영향을 미친다. 영향을 미치지 않게 하려면 `{}` 빈 객체 리터럴에다가 복사를 해서 사용하면 된다.
```javascript
const target = { a:1, b: 2};
const source = { b:4, c: 5};
const returnTarget = Object.assign(target, source);   //source 말고도 뒤에 객체를 더 추가 가능
console.log(target);  // {a:1, b:4, c:5} 출력
console.log(returnTarget) // {a:1, b:4, c:5} 출력
```
### Object.keys
- 객체 데이터의 `property`를 추출해서 배열 데이터로 반환한다.
```javascript
const user = {
  name: 'joseph',
  age: 22,
  email: 'joseph@gmail.com',
}
const keys = Object.keys(user)
console.log(keys) //["name", "age", "email"]출력

console.log(user['email'])  //joseph@gmail.com 출력
const values = keys.map(key => user[key])
console.log(values) // ["joseph", 22, "joseph@gmail"] 출력
```
## 구조 분해 할당
- 비구조화 할당이라고도 한다.
- 데이터의 구조를 분해해서 할당하는 것
```javascript
const user = {
  name: 'joseph',
  age: 22, 
  email: 'joseph@gmail.com'
}
const {name, age, email, address} = user

console.log(`사용자의 이름은 ${name}입니다.`)
// address의 값은 undefined가 나온다.
// 구조분해할당에다가 할당되지 않은 값을 할당할 수 있다. address="korea"
// 원래 객체데이터값이 있으면 재할당해도 무시된다. 위에 address="usa"되어있으면 밑에서 address="korea"해도 무시된다.
// 위의 객체 데이터의 property와 똑같은 이름을 안 써도 된다. name: joseph 이런식으로 하면 밑에서는 joseph으로 사용 가능하다.

/* 배열의 경우에는 {}가 아닌 []로 구조분해할당 가능*/
const [a, b, c, d] = fruits
```

## 전개 연산자
- 마침표 3개가 전개 연산자이다.
- ...를 이용하면 전개해서 문자열로 반환한다.
```javascript
const fruits = ['apple', 'banna', 'cherry']
console.log(...fruits)  // apple banna cherry 출력

function toObject(a,b,c){
  return {
    a:a,
    b:b,
    c:c
  }
}
console.log(toObject(...fruits)) // a:"apple:" b:"banna" c:"cherry" 출력
const fruits = ['apple', 'banna', 'cherry', 'orange']
function toObject(a,b,...c){
  return {
    a:a,  // a,
    b:b,  // b,
    c:c   // c 이런식으로 축약형으로 가능하다. 왼쪽과 똑같은 의미이다.
  }
}
console.log(toObject(...fruits))// 위와 똑같은데 마지막 c에 객체데이터 cherry, orange가 할당된다.
```

## 불변성
- 원시 데이터(불변성): String, Number, Boolean, undefined, null
- 참조형 데이터(가변성): Object, Array, Function
- 원시 데이터의 형태로 데이터가 저장이되면 ex)`let a=1` 1이 저장된 데이터 주소는 변하지 않는다. a=2로 다시 할당하게 되면 1이 저장된 데이터 주소의 1이라는 값이 2로 변하는것이 아니라 다른 데이터 주소에 2가 할당되고 그 공간을 a가 가리키는 형태를 취하게 된다. 즉, 원시 데이터의 형태로 변수를 선언하게되면 변수에 데이터 값을 직접적으로 할당하는 것이 아니고 메모리 주소에 데이터 값을 할당하고 그 메모리 주소를 변수가 가리키는 형태인 것이다. 또한 새로운 변수에 값1을 선언하면 새로운 메모리 주소에 1을 할당하는 것이 아니라 기존에 남아있던 1이 할당되어있던 메모리 주소를 가리키게 된다.
- 참조형 데이터는 원시 데이터와 다르게 가변성이다. 메모리 주소에 할당되어있는 값이 변한다. 또한 서로 다른 변수 a,b가 있다고 할 때 `let a={k:1} let b={k:1}` 로 선언하면 값은 똑같다 하더라도 a,b가 서로 다른 메모리 주소를 가리키고 있고 일치 연산자 `===`로 비교하면 false가 뜬다. 또한 `b=a` 선언 후에 `a.k=2` 를 선언하면 b값 또한 바뀐다. 왜냐하면 a,b가 똑같은 메모리주소를 가리키고 있고 그 주소의 데이터는 참조형 데이터 이므로 1에서 2로 바뀌기 때문이다.

## 얕은 복사와 깊은 복사
- 얕은 복사: 복사를 했을 때 같은 주소를 가리키고 있는 다른 변수에도 영향을 미치는 복사
```javascript
const copyUser = Obeject.assign({}, user)
const copyUser = {...user}
```
- 깊은 복사: 복사를 했을 때 같은 주소를 가리키고 있는 다른 변수에 영향을 미치지 않는 복사
- JS를 이용해서 만들기 쉽지 않기 때문에 lodash 를 이용한다.
```javascript
import _ from 'lodash'
const copyUser = _.cloneDeep(user)  //lodash 이용
```

## 가져오기, 내보내기
- default 로 내보낼 경우에는 따로 이름을 정할 필요가 없고 딱 1개만 가능하다.
- default를 가져왔을 때 함수의 이름을 마음대로 사용할 수 있다.
- default가 아닌 경우에는 이름을 정해주어야 하고 여러개 가능하다. 또한 가져올 때 {} 안에 이름을 넣어야 한다.
- {} 안에 넣을 때 이름을 바꾸고 싶으면 as 를 써야한다.
- *를 이용해서 모든 걸 가져와서 한번에 쓸 수도 있다.
```javascript
/*module.js*/
export default function (data){
  return Object........
}
export const user () {
  .....
}
/*main.js*/
import checkType from './module.js' // default라서 이름이 없지만 checkType으로 마음대로 명명
import { user } from './module.js'  // default가 아니라서 이름을 그대로 가져옴
// import { user as haha } from './module.js' 이렇게 이름 바꿔서 사용 가능
import * as R from './module.js'  // *을 이용해서 한번에 가져와서 R로 명명해서도 가능
```
## Lodash 사용법
- lodash의 메소드 중에 자주 사용하는 메소드를 알아보자.
### .uniqBy
- 한 배열에서 중복되는 내용없이 고유한 값으로 줄여준다.
```javascript
console.log('uniqBy', _.uniqBy(user, 'userId'))
// user배열에서 userId의 값이 중복된 것들을 없애고 하나만 남긴다.
```


### .unionBy
- 여러개의 배열을 합쳐서 중복되는 내용없이 고유한 값으로 줄여준다.
```javascript
console.log('unionBy', _.unionBy(user1, user2, 'userId'))
// user1, user2 를 합친후 배열에서 userId의 값이 중복된 것들을 없애고 하나만 남긴다.
```
### .find
- 값을 찾아서 반환한다.

```javascript
const founUser = _.find(users, { name: 'Amy' })
```
### .findIndex
- 값을 찾아서 그 인덱스를 반환한다.
```javascript
const founUserIndex = _.findIndex(users, { name: 'Amy' })
```

### .remove
- 해당 데이터를 찾아서 삭제한다.
```javascript
_.remove(users, {name: 'joseph'}) 
```
## JSON
- JavaScript Object Notation
- 자바스크립트의 객체 표기법
> SON(제이슨[1], JavaScript Object Notation)은 속성-값 쌍(attribute–value pairs), 배열 자료형(array data types) 또는 기타 모든 시리얼화 가능한 값(serializable value) 또는 "키-값 쌍"으로 이루어진 데이터 오브젝트를 전달하기 위해 인간이 읽을 수 있는 텍스트를 사용하는 개방형 표준 포맷이다. 비동기 브라우저/서버 통신 (AJAX)을 위해, 넓게는 XML(AJAX가 사용)을 대체하는 주요 데이터 포맷이다. 특히, 인터넷에서 자료를 주고 받을 때 그 자료를 표현하는 방법으로 알려져 있다. 자료의 종류에 큰 제한은 없으며, 특히 컴퓨터 프로그램의 변수값을 표현하는 데 적합하다.
- 쌍따옴표만 사용가능하다.
- 문자데이터이다. 실제로는 객체데이터를 담고있어도 문자데이터 형식으로 저장이 되어있다. 그래서 이를 자바스크립트에서 쓰기 위해서는 메소드를 이용해서 객체데이터화 시켜 사용할 수 있다.
```javascript
import myData from './myData.json'  //json파일로부터 가져왔지만 문자데이터이다.
const str = JSON.stringify(user)  // JSON은 전역객체, stringify를 이용해서 문자데이터를 str에 저장
const obj = JSON.parse(str) // 문자데이터를 parse를 이용해서 객체데이터화
```

## Storage
> localStorage 읽기 전용 속성을 사용하면 Document 출처의 Storage 객체에 접근할 수 있습니다. 저장한 데이터는 브라우저 세션 간에 공유됩니다. localStorage는 sessionStorage와 비슷하지만, localStorage의 데이터는 만료되지 않고 sessionStorage의 데이터는 페이지 세션이 끝날 때, 즉 페이지를 닫을 때 사라지는 점이 다릅니다. ("사생활 보호 모드" 중 생성한 localStorage 데이터는 마지막 "사생활 보호" 탭이 닫힐 때 지워집니다.)

- localStorage에 value값은 문자데이터로 저장하는걸 권고.

> 아래 코드는 현재 도메인의 로컬 Storage 객체에 접근한 후, Storage.setItem() (en-US)을 사용해 항목 하나를 추가합니다.
localStorage.setItem('myCat', 'Tom');
Copy to Clipboard
위에서 추가한 localStorage 항목을 읽는 법은 다음과 같습니다.
const cat = localStorage.getItem('myCat');
Copy to Clipboard
그리고 제거는 아래와 같습니다.
localStorage.removeItem('myCat');
Copy to Clipboard
localStorage 항목의 전체 제거 구문입니다.
localStorage.clear();
Copy to Clipboard

### Lowdb
- 위의 방법 이외에 lodash의 lowdb를 이용해서 보다 쉽게 localstorage를 db 처럼 쓸수가 있다. 자세한건 검색해서 찾아보자.

## OMDb API
- open movie database
- api key를 받아야하는데 공식사이트에서 받을 수 있다.

### query string
- 문자를 가지고 검색하는 문법
- 주소?속성=값&속성=값&속성=값

### axios
- query string 을 통해 OMDb api를 이용해서 문자데이터들을 얻었는데 그 데이터를 이용하는데 필요한 패키지
```javascript
import axios from 'axios'

function fetchMovies() {
  axios
    .get('https://www.omdbapi.com/?apikey=7035c60c&s=frozen')
    .then((res) => {
      console.log(res)
      const h1El = document.querySelector('h1')
      const imgEl = document.querySelector('img')
      h1El.textContent = res.data.Search[0].Title
      imgEl.src = res.data.Search[0].Poster
    })
}
fetchMovies()
```
## 정규표현식(RegExp)
- Regualr Expression

### 역할
- 문자 검색
- 문자 대체
- 문자 추출

### 테스트사이트
- https://regexr.com/

### 정규식 생성
```js
// 생성자
new RegExp('표현', '옵션')
new RegExp('[a-z]', 'gi')

// 리터럴
/표현/옵션
/[a-z]/gi // g 면 대문자 구분, gi면 대문자무시
```

```js
const str = ` 
010-1234-5678
joseph@gmail.com
https://www.omdbapi.com/?apikey=7035c60c&s=frozen
The quick brown fox jumps over the lazy dog
abbaaccdddd
`

const regexp = new RegExp('the', 'g')
console.log(str.match(regexp))

// const regexep = /the/gi  도 가능
```


***
#### 기타 내용
- prototype으로 지정된 메소드는 언제, 어디서든 사용할 수 있다.
- Object: 전역객체이며 프로토타입이 아니기 때문에 객체 데이터에 직접적으로 사용이 불가능하다.
- Object.??? : 정적 메소드, 스테틱 메소드