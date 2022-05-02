# TypeScript Compiler

## Compilation Context
> 컴파일 컨텍스트는 근본적으로 집단에서 사용하는 용어이며 타입스크립트는 유효한 것을 분석하고 해석합니다. 어떤 파일의 정보와 함께 컴파일 컨텍스트에는 사용중인 컴파일러 옵션에 대한 정보가 들어있습니다. 이 논리그룹을 정의하는 가장 좋은 방법은 tsconfig.json 파일을 사용하는 것 입니다.

- 타입스크립트 컴파일러가 어떻게 js로 컴파일할것인지에 대한 옵션, 정보를 담고 있는 것이 Compilation Context 이고 이는 tsconfig.json 파일에 담아서 사용한다.

## tsconfig schema
- https://json.schemastore.org/tsconfig : tsconfig schemda의 전체 내용을 담고 있는 사이트
- 최상위 프로퍼티
  - compileOnSave
  - extends
  - compileOptions  어떤 설정으로 컴파일 할것인지 자세히 들어있다.
  - files     이 3개를 묶어서 어떤 파일을 컴파일할건지 결정
  - include  이 3개를 묶어서 어떤 파일을 컴파일할건지 결정
  - exclude  이 3개를 묶어서 어떤 파일을 컴파일할건지 결정
  - references
  - ~~typeAcquisition~~
  - ~~tsNode~~

  ## compileOnSave
- true / false(default false)
- 밑에서만 작동한다. 그래서 엄청 중요한 property는 아니다.
  - visual studio 2015 with typescript 1.8.4이상
  - atom-typescript 플러그인

  ## extends
- 파일경로명을 명시해서 상속받을 수 있다.
- "extends": "파일경로명" -ex)`"extends" : "./base.json"`
- 2.1 버전 이상에서만 사용 가능하다.
- 깃허브 tsconfig / bases 가면 여러가지 형태의 노드를 사용할 수 있는 타입스크립트 설정이 들어있다.
- npm install --save-dev @tsconfig/deno 이를 통해 증명된 여러가지 설정들을 사용할 수 있다.
  - "extends": "@tsconfig/deno/tsconfig.json"

## files, include, exclude
- 프로젝트 안에있는 어떤 파일을 컴파일 할 것인지 결정한다.
- 셋다 설정이 없으면 전부다 컴파일 하려고한다.
- files
  - 상대 혹은 절대경로의 리스트 배열이다.
  - exclude보다 쎄다
- include, exclude
  - glob패턴 (마치 .gitgnore)
  - include
    - exclude 보다 약하다.
    - *같은것을 사용하면 .ts/ .tsx/ .d.ts만 include (allowJS - 이걸 켜야 js파일들도 컴파일 될것이다.)
  - exclude
    - 설정안하면 4가지 (node_modules, bower_components, jspm_packages, <outDir>)를 dafualt로 제외한다.
    - <outDir>은 항상 제외한다. (include에 있어도)

## compileOptions-typeRoots, types
- 타입이란 일반적으로 타입시스템을 의미하는것이 아니고 라이브러리를 사용했을때 자바스크립트기 때문에 타이핑이 안되어있는데 그 타입을 지정해주어야하는데 타입스크립트가 안했고 서드파티를 이용해서 타입을 제공해주고 있었다.
  - 예시로 리엑트를 받아서 타입스크립트에서 `import React from "react" 를 치면 에러를 알려준다.
- @types
  - ts 2.0부터 사용가능해진 내장 type deninition 시스템
  - 아무설정을 안하면?
    - node_modules/@types 라는 모든 경로를 찾아서 사용
  - typeRoots 를 사용하면?
    - 배열 안에 들어있는 경로들 아래서만 가져온다
  - types를 사용하면?
    - 배열 안의 모들 혹은 ./node_modules/@types/안의 모듈 이름에서 찾아온다.
    - [] 빈 배열을 넣는다는건 이 시스템을 이용하지 않겠다는 것.
  - typeRoots와 types를 같이 사용하지 않는다.

  ## compileOptions -target과 lib
- 프로젝트 설정의 기본이 되는 중요한 요소이다.
- target
  - 빌드의 결과물을 어떤 버전으로 할 것인지 지정하는 것
  - 지정을 안하면 es3이다.
- lib
  - 기본 type definition 라이브러리를 어떤것을 사용할것인지 지정
  - lib를 지정하지 않았을 때
    - target이 es3 이면 디폴트로 lib.d.ts를 사용한다.
    - target이 es5 이면 디폴트로 dom, es5, scripthost 를 사용한다.
    - target이 es6 이면 디폴트로 dom, es6, dom.literable, scripthost를 사용한다.
  - lib 를 지정하면 그 lib배열로만 라이브러리를 사용한다.
    - 빈[] => 'no definition found 어쩌구저쩌구'

 ## compileOptions - outDir, outFile, rootDir
- 컴파일 한 js를 생성하는 곳에 영향을 준다. 

## compileOptions - strict
- 여러개의 엄격한 체크 옵션에 관한 프로퍼티
- --nolmplicitAny
  - 명시적이지 않게 any타입을 사용하여 표현식과 선언에 사용하면 에러를 발생
  - 타입스크립트가 추론을 실패한 경우 any가 맞으면 any라고 지정하라.
  - 아무것도 쓰지 않으면 에러를 발생
  - 이 오류를 해결하면 any라고 지정되어있지 않는 경우는 any가 아닌것이다.(타입추론이 되었으므로)
  - 이를 사용할 때 인덱스 객체에 인덱스 signature가 없는 경우 오류가 발생하는데 이를 예외 처리한다.
  - obj['foo']로 사용할 때, 인덱스 객체라 판단하여, 타입에 인덱스 시그니처가 없는 경우, 에러를 발생시킨다.
  - 이때 suppresslmplictAnyIndexErrors 옵션을 사용하면 이런경우 예외로 간주하여 에러를 발생시키지 않는다.
  
- --nolmplicitThis
  - 명시적이지 않게 any 타입을 사용하여 this 표현식에 사용하면 에러를 발생시킨다.
  - 첫번째 매개변수 자리에 this를 놓고 this에 대한 타입을 어떤것이라도 표현하지 않으면 nolmplicitAny가 오류를 발생시킨다.
  - javascript에서는 매개변수에 this 를 넣으면 이미 예약된 키워드라 syntaxerror를 발생시킨다.
  - call/ apply/ blind 와 같이 this를 대체하여 함수 콜을 하는 용도로도 쓰인다.
  - 그래서 this를 any로 명시적으로 지정하는 것이 합리적이다.(물론 구체적인 사용처가 있으면 타입을 표현하기도 한다.)
  - class에서 this를 사용하면서 nolmplicitThis와 관련된 에러가 나지 않는다.
  - class에서 constructor 를 제외한 멤버 함수의 첫번째 매개변수도 일반 함수와 마찬가지로 this를 사용할 수 있다.

- --strictNullChecks
  - null 및 undefined값이 모든 유형의 도메인에 속하지 않으며, 그 자신을 타입으로 가지거나 any 일 경우에만 할당이 가능하다.
  - 한가지 예외는 undefined에 void할당 가능
  - strictNullchecks를 적용하지 않으면
    - 모든 타입은 null, undefined 값을 가질 수 있다.
    - string으로 타입을 지정해도 null 혹은 undefined 값을 할당할수 있다는 것이다.
  - 이를 적용하면
    - 모든 타입은 null, undefined값을 가질 수 없고 가지려면 union type을 이용해서 직접 명시해야 한다.
    - any타입은 null과 undefinned 를 가진다. 예외적으로 void 타입의 경우 undefined를 가진다.
  - 이것을 적용하지않고 어떤 값이 null undefined를 가진다는것을 암묵적으로 인정하고 계속 사용하다보면 정확하게 어떤 타입이 오는지를 개발자 스스로가 간과할 수 있다.
  - 정말로 null과 undefined를 가질 수 있는 경우, 해당 값을 조건부로 제외하고 사용하는 것이 좋다.
  - 이 옵션을 켜고 사용하는 경우 사용하려는 함수를 선언할 때 부터 매개변수와 리턴값에 정확한 타입을 지정하려는 노력을 기울여야 하고 기울이게 될것이다.

- --strictFunctionTypes
  - 함수 타입에 대한 bivariant 매개변수를 비활성화한다.
  - 반환 타입은 공변적이어야 하고 인자타입은 반공변적이어야 한다.
  - 타입스크리브에서는 인자타입은 공변적이면서 반공변적인것이 문제이다.
  - 이 문제를 해결하는 옵션이 strictFunctionTypes 
  - 옵션을 켜면 에러가 안나던걸 에러가 나게 한다.

- --stricPropertyInitialization
  - 정의 되지 않은 클래스의 속성이 생성자에서 초기화 되었는지 확인한다. 이 옵션을 사용하려면 --strictNullChecks를 사용하도록 설정해야 한다.

- --strictBindCallApply
  - bind, call, apply 에 대한 더 엄격한 검사 수행
    - function의 내장함수인 bind, call, apply를 사용할 때 엄격하게 체크하도록 하는 옵션이다.
    - bind는 해당 함수안에서 사용할 this와 인자를 설정해주는 역할을 하고 call 과 apply는 this와 인자를 설정한 후 실행까지 한다.
    - call과 apply 는 인자를 설정하는 방식에서 차이점이 있다.
      - call은 함수의 인자를 여러인자의 나열로 넣어서 사용하고 apply는 모든 인자를 배열 하나로 넣어서 사용한다.

- --alwaysStirct
  - 각 소스 파일에 대해 js 의 strict mode로 코드를 분석하고 엄격하게 사용을 해제한다.

# Interfaces

## What are Interfaces
- 인터페이스란 타입을 만들어 내는 방식이다.
```ts
interface Person1 {
  name: string;
  age: number;
}


function hello1(person: Person1 ): void {
  console.log(`안녕하세요! #{person.name} 입니다`);
}

const p1: Person1 = {
  name: "Mark",
  age: 39
};

hello1(p1);
```
## optional property
- ?를 통해 인수에 값을 넣어도, 안넣어도 되게 할 수 있다.
```ts

interface Person2 {
  name: string;
  age?: number; // 없을수도 있으 age뒤에 ?
}

function hello2(person: Person2): void {
  console.log(`안녕하세요 ${person.name} 입니다.`)
}

hello2({ name: "Mark", age: 39});
hello2({ name: "Anna"});
```

```ts
interface Person3 {
  name: string;
  age?: number;
  [index: string]: any  //대신 어떤 프로퍼티가 와도 괜찮다는 뜻
}

function hello3(person: Person3): void {
  console.log(`안녕하세요! ${person.name} 입니다`)
}

const p31: Person3 = {
  name: "Mark",
  age: 39
};

const p32: Person3 = {
  name: "Anna",
  systers: ['Sung', "Chan"]
};

const p33: Person3 = {
  name: 'bokdaegi',
  father: p31,
  mother: p32
}

hello3(p31)
```

## function in interface
```ts
interface Person4 {
  name: string;
  age: number;
  hello(): void;
}

const p41: Person4 = {
  name: 'Mark',
  age: 39,
  hello: function(): void { //function(): 없애도 똑같음
    console.log(`안녕하세요 ${this.name} 입니다.`);
  }
}

p41.hello();
```

## class implements interface
```ts
interface IPerson1 {
  name: string;
  age?: number;
  hello(): void;
}

class Person implements IPerson1 {
  name: string;
  age?: number | undefined;

  constructor(name: string){
    this.name = name;
  }
  hello(): void{
    console.log(`안녕하세요! ${this.name} 입니다.`);
  }
}

const person: IPerson1 = new Person("Mark");
person.hello();
```

## interface extends interface
```ts
interface IPerson2 {
  name: string;
  age?: number;
}

interface IKorean extends IPerson2 {
  city: string;
}

const k: IKorean = {
  name: "joseph",
  city: "seoul",
};

HTMLDivElement 
```

## function interface
```ts
interface HelloPerson {
  (name: string, age?: number): void;
}

const helloPerson: HelloPerson = function(name: string, age: number) {  // HelloPerson 에러, age?가 와야함. 안되는 이유는 age? 는 number | undefined 타입인데 age:number 로 하면 number만 타입이기 때문이다.
  console.log(`안녕하세요 #{name}입니다.`);
}

helloPerson('Mark', 39);
```

## Readonly Interface Properties
- 읽기 전용 속성이다. 
```ts
interface Person8 {
  name: String;
  age?: number;
  readonly gender: string;
}

const p81: Person8 = {
  name: "Mark",
  gender: "male"
};

p81.gender = "female";  // 오류
```

## type alias vs interface
- type alias
```ts
type EatType = (food: string) => void;
```
- interface
```ts
interface IEat {
  (food: string): void;
}
```
- array
```ts
type PersonList = string[]; // type alias
interface IPersonList { //interface
  [index: number]: string;
}
```