# Part5. TypeScript Essentials

## TypeScript 란 무엇인가
- 프로그래밍 언어이다.
- 컴파일언어 이지만 전통적인 컴파일 언어와는 다른 점이 있다. 그래서 Transpile이라는 용어를 사용하기도 한다.
- typescript로 작성한 것을 바로 js 실행환경에서 사용할 수는 없다. typescript compiler가 필요하기 때문이다.

## TypeScript 설치 및 사용
- npm i typescript -g // 모든 장소에서 쓸 수 있게
- node_modules/.bin/tsc // g를 안붙이면 그 프로젝트안에 생김
- tsc source.ts // source.ts를 컴파일해서 javascript파일로 바꾸어줌
### 글로벌 사용법
```
npm i typescript -g   // 글로벌하게 타입스크립트가 설치
tsc test.ts // test.ts 를 컴파일해서 test.js가 생성
tsc   // 이것만 치면 컴파일이 안된다. 어떻게 컴파일을 할지 기본적인 파일을 같은 프로젝트에 넣어 주어야 한다.
tsc --init  // tsconfig.json은 어떻게 컴파일을 할지 정보를 담고있는 default인데 이 파일을 생성한다.
tsc   // 위에서 tsconfig.json을 만들었으므로 이제 같은 디렉토리에있는 파일이 컴파일이 된다.
tsc -w  // 실시간으로 파일이 수정될 때마다 컴파일이 된다.
```
### 프로젝트 단위 사용법
```
npm uninstall typescript -g // 글로벌하게 설치되었던 타입스크립트를 지운다.
npm init  // npm을 시작하는 명령어이다. -y를 뒤에 붙이면 모든 질문에 yes로 선택되어서 바로 시작되고 package.json   파일이 생성
npm i typescript  // 타입스크립트를 설치(글로벌이 아님) package.json 을 열어보면 typescript버전이 보이고 node_modules 디렉토리 생성
npx tsc --init  // tsconfig.json 파일 생성
npx tsc // 디렉토리에 있는 ts파일을 컴파일해서 js파일로 생성
npx tsc -w  // 실시간으로
npm run build // package.json파일에 가서 script부분을 "build": "tsc" 로 바꿔주면 이렇게도 가능.
npm run build:watch // 실시간으로
```

## VS Code 설치 및 설정
- VS Code에 컴파일러가 내장되어 있다.
- 내장된 컴파일러 버전은 VS Code가 업데이트 되면서 올라간다.
  - 그래서 컴파일러 버전과 VS Code의 버전은 상관 관계가 있다.
- 내장된 컴파일러를 선택할 수 있고 직접 설치한 컴파일러를 선택할 수도 있다.

## First Type Annotation
- type annotation: 타입스크립트가 가진 고유의 기능이다. 
- 변수에 타입을 지정해주는 것이 type annotation이다.
```typescript
let a = "Mark";
a = 7;  // 오류가 난다. 위에서 a는 string으로 선언되어있기 때문에 타입이 string으로 지정되었기 때문이다.
let a: number;  // 이런식으로 타입을 지정해 줄 수 있다.
```

## TypeScript Types vs JavaScript Types
- TypeScript: Static Types, JavaScript: Dynamic Types
- 타입스크립트는 개발하는 중간에 타입을 체크하고 자바스크립트는 런타임에 돌입해야만 잘못된것을 알 수 있다.
- 자료형의 경우에 Javascript의 기본 자료형6개를 포함한다.(ECMAScript 표준)
  - Boolean, Number, String, Null, Undefined, Symbol, Array: object형
- 프로그래밍을 도울 몇가지 타입이 더 제공된다.
  - Any, Void, Never, Unknown, Enum, Tuple: object형

## Primitive Types
- 오브젝트와 레퍼런스 형태가 아닌 실제 값을 저장하는 자료형이다.
- 프리미티브 형의 내장함수를 사용가능한것은 자바스크립트의 처리방식 덕분
- bollen, number, string, symbol, null, undefined
<br>
- literal 값으로 프리미티브 타입의 서브 타입을 나타낼 수 있다.
- 래퍼 개체로도 만들 수 있다. 하지만 권고하지 않는다.
```javascript
new Boolean(false);
new String('world');
new Number(42);
```

### Type Casing
- TypeScript의 핵심 primitive types는 모두 소문자이다.
- Number, String, Boolean, Symbol 또는 Obejct유형은 위에서 권장한 소문자 버전과 동일하지 않고 primitives를 나타내지 않으며 타입으로 사용해서는 안된다.
- number, string, boolean, symbol, object 타입을 사용해야 한다.

## number
- javascript와 같이 모든 숫자는 부동 소수점 값이다.
- 16진수, 10진수, 리터럴 외에도 2진수, 8진수를 지원한다.
- NaN도 숫자취급
```ts
let decimal: number = 6;

let hex: number = 0xf00d;

let binary: number = 0b1010;

let octal: number = 0o744;

let notAnumber: number = NaN;

let underscoreNum: number = 1_000_000;  //이렇게 써도 가능

```

## string
- 텍스트 형식을 참조하기 위해 'string' 형식을 사용한다.
- JS와 마찬가지로 TS는 문자열 데이터를 둘러싸기 위해 큰따옴표`"` 나 작은 따옴표`'`를 사용한다.
- `&{}` 기능을 JS와 같이 제공한다.

## symbol
- ECMAScript 2015부터 추가된 Symbol이다.
- Symbol을 함수로 사용해서 symbol타입을 만들어 낼 수 있다.
- 프리미티브 타입의 값을 담아서 사용한다.
- 고유하고 수정불가능한 값으로 만들어준다.
```ts
console.log(Symbol("foo") === Symbol("foo"));

const sym = Symbol();

const obj = {
  [sym]: "value",
};

obj[sym]  // 이렇게 해야만 접근이 가능하다. 문자열 넣으면 안댐
```

## null & undefined
- TS에서 이 둘은 실제로 각각 undefined, null 이라는 타입을 가진다
- void와 마찬가지로 그 자체로는 유용하지 않다.
- 둘 다 소문자만 존재한다.
- 모든 타입의 서브타입으로 존재한다. (tsconfig 설정을 해주지 않으면 즉, 컴파일 옵션을 설정하지 않으면)
  - number에 null, undefined를 할당 할 수있다는 뜻이다.
  - 컴파일 옵션에서 `--strictNullChecks` 사용하면 null, undefiendsms void나 자기 자신들에게만 할당
  - 이 경우에 null과 undefiend를 할당 할 수 있게 하려면 union type을 이용해야 한다.
```ts
let union: string | null = null; // 이게 유니온 타입 스트링 타입이면서 null 타입이기도 하다.
```

### null in javascript
- null 이라는 값으로 할당된 것을 null 이라고 한다.
- 무언가가 있는데, 사용할 준비가 덜 된 상태
- null이라는 타입은 null 이라는 값만 가질 수 있다.
- 런타임에서 typeof연산자를 이용해서 알아내면 object 이다.
### undefined in javascript
- 값을 할당하지 않은 변수는 undefined 라는 값을 가진다.
- 무언가가 아예 준비가 안된 상태
- object의 property가 없을 때도 undefined이다.
- 런타입에서 typeof 연산자를 이용해서 알아내면, undefined이다.

## object
```ts
const person1 = { name: `joseph`, age:22};

const person2 = Object.create({ name: "joseph", age:22}); // 유니온 타입 object, null 타입 둘 다
```
- primitive type이 아닌것을 나타내고 싶을 때 사용하는 타입
- primitive type이 아닌 것들: number, string, boolean, symbol, null, undefiend

## array
```ts
let list: number[] = [1,2,3];
let list1: Array<number> = [1,2,3];
let list: (number | string)[] = [1,2,3, "4"]; //  이런식으로 넘버와 스트링 두개의 타입으로도 가능 하지만 어디부터 number 이고 어디서부터 string 인지 알 수 없어서 tuple이라는 타입이 나오게 되었다.
```

## tuple
```ts
let x: [string, number];

x = ["hello", 22];

x = [10, "mark"]; // 오류

x[2]; // 배열의 길이보다 길어서 오류

const person: [string, number] = ["mark", 33];

const [first, second, third] = person;  // 배열의 길이보다 길어서 오류
```

## any
- 어떤것이 된다는 타입, 아닐 때도 있다.
- 이걸 최대한 쓰지 않는게 핵심이다.
- 컴파일 타임에 타입 체크가 정상적으로 이루어지지 않기 때문이다.
- 컴파일 옵션중에는 any를 써야하는데 쓰지 않으면 오류 메세지를 띄우는 옵션도 있다.(nolmpilcitany)
- any는 계속해서 개체를 통해 전파된다. (서로 연산하거나 대입하는 과정에서 any타입으로 된다.)
- 편의에 의해서 쓸 수 있지만 타입 안전성을 잃는다.
- 필요하지 않는 경우에는 any를 사용하지 않도록 해야한다.
```ts
function returnAny(message: any): any { // : any 이걸 입력하지 않으면 에러 (nolmpilcitany)
  console.log(message);
}
const any1 = returnAny("리턴은 아무거나");

any1.toString();
```


