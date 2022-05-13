## unknown
- 응용 프로그램을 작성할 때 모르는 변수의 타입을 묘사해야 할 수도 있다.
- 이러한 상황은 동적 컨텐츠(사용자나 api의 모든 값을 의도적으로 수락해야만 할 때)를 다룰 때 생긴다.
- 이 경우에 컴파일러와 미래의 코드를 읽는 사람에게 이 변수가 무엇이든 될 수 있음을 알려주는 타입을 제공해야 하므로 unknown타입을 제공한다.
- ts 3.0버전부터 지원
- any와 짝으로 any 보다 Type-safe한 타입
  - any와 같이 아무거나 할당 할 수 있다.
  - 컴파일러가 타입을 추론할 수 있게끔 타입의 유형을 좁히거나 타입을 확정해주지 않으면 다른 곳에 할당할 수 없다.
- unknown 타입을 사용하면 runtime error 를 줄일 수 있을 것 같다.
  - 사용 전에 데이터의 일부 유형의 검사를 수행해야 함을 알리는 api에 사용할 수 있을것같다.
```ts
declare const maybe: unknown;

const aNumber: number = maybe;

if(maybe === true){
  const aBoolean: boolean = maybe;  //maybe
  
  const aString: string = maybe;  // 위에서 bollean타입으로 정의되서 여기서는 오류
}
if(typeof maybe === 'string') {
  const aString: string = maybe;  // 위에서 string타입으로 정의되서
  const aBoolean: boolean = maybe;  // 여기서는 오류
}
```

## never
- never 타입은 모든 타입의 subtype이며 모든 타입에 할당 할 수 있다.
- 하지만 never에는 그 어떤 것도 할당할 수 없다.
- any 조차도 never에게 할당할 수 없다
- 잘못된 타입을 넣는 실수를 막고자 할 때 사용하기도 한다.
```ts
function error(message: string): never {
  throw new Error(message);
}

function fail() {
  return error('failed');
}

function infiniteLoop(): never {
  while(true) {

  }
}

declare const a: string | number;

if(typeof a != 'string') {
  a;

}

type Indexable<T> = T extends string ? T & {[index: string]: any } : never;

type ObjectIndexable = Indexable<{}>;
```

## void
- return부분에 달아서 아무곳에서도 사용하지 않겠다는 뜻이다.
```ts
function returnVoid(message: string): void {
  console.log(message);

  return undefined; // void에는 유일하게 undefined만 할당 가능
}

returnVoid('리턴이 없다');

```

## 작성자와 사용자의 관점으로 코드 바라보기
- 타입시스템
  - 컴파일러에게 사용하는 타입을 명시적으로 지정하는 시스템
  - 컴파일러가 자동으로 타입을 추론하는 시스템
- 타입스크립트의 타입 시스템
  - 타입을 명시적으로 지정할 수 있다.
  - 타입을 명시적으로 지정하지 않으면, 타입스크립트 컴파일러가 자동으로 타입을 추론
- 타입이란 해당 변수가 할 수 있는 일을 결정한다.
- 함수 사용법에 대한 오해를 야기하는 자바스크립트
```js
function f2(a) {
  return a * 38;
}
console.log(f2(10));  //380 출력 정상적, 의도적으로 작동
console.log(f2('mark')) // Nan 출력, 작성자의 의도대로 함수가 사용되지 않음.
```
- 타입스크립트의 추론에 의지하는 경우
```ts
function f3(a){
  return a * 38;  // a를 명시적으로 타입을 지정하지 않았기 때문에 any로 추론된다.
}
console.log(f3(10));  // 380 출력
console.log(f3('mark') + 5); // NaN출력, 이 또한 작성자 의도대로 함수가 사용되지 않음
```
- 위와 같이 매개변수 a가 타입이 지정되지 않아서 혹은 추론에 의해 any로 지정되면 작성자의 의도대로 함수가 사용되지 않을 수 있다. 그래서 nolmplicitAny 옵션이 있다. 타입을 명시적으로 지정하지 않은 경우 타입스크립트가 any라고 판단하게 되면 컴파일 에러를 발생시켜 명시적으로 지정하도록 유도한다.
- nolmplicitAny에 의한 방어
```ts
function f3(a){
  return a * 38; 
}
//위에서 any로 추론되어 컴파일 에러를 일으킨다
console.log(f3(10)); 
console.log(f3('mark') + 5); 
```
```ts
function f4(a: number){
  if (a>0){
  return a * 38;
  }
}
console.log(f4(10)); // 여기서는 리턴이 number로 추론되어서 190이 나온다.
console.log(f4(-5) +5); // a가 음수면 리턴이 없다. 그래서 f4(-5) = undefined타입 이므로 NaN 출력된다. 이는 undefined타입과 number타입의 연산이 진행된건데 undefined타입을 number로 취급하고 연산한셈이다.
```
- strictNullChecks옵션을 키면 모든 타입에 자동으로 포함되어있는 null 과 undefined를 제거해준다.
```ts
function f4(a: number){ // 함수는 number | undefined 타입 형태로 추론된다.
  if (a>0){
  return a * 38;
  }
}
/*사용자는 사용법에 맞게 숫자형을 사용하여 함수를 실행했다. 해당 함수의 리턴 타입은 number | undefined 이기 때문에
타입에 따르면 이어진 연산을 바로 할 수 없다. 컴파일 에러를 고쳐야 하기 때문에 사용자와 작성자가 논의 해야한다. */
console.log(f4(10));
console.log(f4(-5) +5); // error : undefined와 number타입은 서로 연산 불가. strictNullChecks 옵션을 켰기 때문이다.
```
- 명시적으로 리턴타입을 지정해야할까?
```ts
function f5(a: number): number {
  if (a >0) {
    return a * 38;
  }
}
```
- nolmplicitReturns 옵션을 켜면 함수 내에서 모든 코드가 값을 리턴하지 않으면 컴파일 에러를 발생시킨다. 위에서 if문을 충족시키지 않을 때에도 return 을 시켜줘야한다.
- 매개변수 object가 들어오는 경우
```ts
function f6(a) {
  return `이름은 ${a.name} 이고, 연령대는 ${Math.floor(a.age/10) *10} 대 입니다.`;
}
console.log(f6({ name: 'mark', age:22})); // 이름은 mark 이고, 연령대는 30대이다.
console.log(f6('mark'));  // 이름은 undefined 이고, 연령대는 NaN이다. 이걸 막기위해 오브젝트 타입을 지정해야한다.
```
```ts
function f6(a: {name: string; age: number}): string {
  return `이름은 ${a.name} 이고, 연령대는 ${Math.floor(a.age/10) *10} 대 입니다.`;
}
console.log(f6({ name: 'mark', age:22})); 
console.log(f6('mark'));

```
- 나만의 타입을 만드는 방법 (위에서 처럼 오브젝트 타입을 일일이 치면 번거로우므로)
```ts
interface PersonInterface {
  name: stirng
  age: number;
} // 이렇게 선언해놓으면

function f8(a: PersonInterface): string { // 이렇게 타입명시 가능
  ......
}
```

## Strutural Type System vs Nominal Type System
- Strutural Type System: 구조가 같으면 같은 타입이다. - 타입스크립트
- Nominal Type System: 구조가 같아도 이름이 다르면 다른타입니다. - c언어, java...
- duck typing: 어떤 새가 오리처럼 걷고, 헤엄치고, 꽥꽥거리면 나는 그 새를 오리라고 부를것이다. 라는 형태의 타이핑 기법

## 타입 호환성
- 같거나 서브 타입인 경우 할당이 가능하다. (공변)
- 함수의 매개변수 타입만 같거나 슈퍼타입인 경우 할당이 가능하다. (반병)
- strictFunctionTypes옵션을켜면 함수를 할당할 시에 함수의 매개변수 타입이 같거나 슈퍼타입인 경우가 아닌경우 에러를 통해 경고한다.

## 타입 별칭(type alias)
- interface 랑 비슷해보인다.
- primitive, union type, tuple, function이런 것들을 별칭하는 것
- 기타 직접 작성해야하는 타입을 다른 이름을 지정할 수 있다.
- 만들어진 타입의 refer 로 사용하는 것이지 타입을 만드는것은 아니다.
- Aliasing Primitive
```ts
type MyStringType = string; // string타입을 MyStringType이라는 이름으로 별칭하고 
const str = 'world';
let myStr: MyStringType = 'hello';  // 여기서 MyStringType으로 타입 명시
myStr = str;
```
- Aliasing 다른 타입들도 똑같이 type ~~~~ 로 별칭 할 수 있다.
- Aliasing Function
```ts
type EatType = (food: string) => void;
```