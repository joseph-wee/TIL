# Classes

## What are Classes
- object를 만드는 청사진, 설계도
- 클래스 이전에 object를 만드는 기본적인 방법은 function
- Javascript에도 class는 es6부터 사용가능
- OOP 를 위한 초석
- TypeScript에서는 클래스도 사용자가 만드는 타입의 하나

## Quick Start - calss
- class 키워드를 이용하여 클래스를 만들 수 있다.
- class 이름은 보통 대문자를 이용한다.
-  new 를 이요하여 class 를 통해 object를 만들 수 있다.
- constructor를 이용하여 object를 생성하면서 값을 전달할 수 있다.
- this를 이용해서 만들어진 object를 가리킬수 있다.
- js로 컴파일 되면 es5의 경우 function으로 변경된다.
```ts
class Person {
  name;
  
  constructor(name: string) {
    this.name = name;
  }
}

const p1 = new Person("Mark");

console.log(p1);
```

## constructor & initialize
- 생성자 함수가 없으면, 디폴트 생성자가 불린다.
- 프로그래머가 만든 생성자가 하나라도 있으면, 디폴트 생성자는 사라진다.
- strict모드에서는 프로퍼티를 선언하는 곳 또는 생성자에서 값을 할당해야한다.
- 프로퍼티를 선언하는 곳 또는 생성자에게 값을 할당하지 않는 경우에는 !를 붙여서 위험을 표현한다.
- 클래스의 프로퍼티가 정의되어 있지만, 값을 대입하지 않으면 undefined이다.
- 생성자에는 async를 설정할 수 없다.
```ts
class Person {
  name: string = "Mark";  
  age!: number; //느낌표는 값이 할당되지않아도 의도적으로 한것이라는 표현이다.
  
  constructor(age?: number) {
    if(age == undefined){
      this.age = 20;
    }
    else {
      this.age = age;
    }
  }

}

/*위에서 프로퍼티에 초기화를 설정해주지 않으면 오류가 뜬다. 왜냐하면 age를 보면 타입이 넘버로
설정 되어있는데 밑에서 consol.log(p1.age)를 하면 age의 타입은 분명 넘버로 되어있는데
값이 할당되어있지 않으므로 undefined가 뜬다. 이는 앞서 설정한 age의 타입이 넘버로되어있는
것에 위배되므로 오류가 뜨는 것이다.*/
const p1 = new Person(39);
const p2 = new Person();
console.log(p1);
p1.age = 39;
console.log(p1.age)
```

## 접근 제어자 (Access Modifiers)
- 접근 제어자에는 public, private, protected가 있다.
- 설정하지 않으면 public 이다.
- 클래스 내부의 모든 곳에(생성자, 프로퍼티, 메소드) 설정 가능하다.
- private로 설정하면 클래스 외부에서 접근 할 수 없다.
- 자바스크립트에서 private를 지원하지 않아 오랫동안 프로퍼티나 메소드 이름 앞에_를 붙여서 표현했다.
  - 요즘에도 관행처럼 하고있기는한데 특별한 의미가 있는 것은 아님.

## initailization in constructor parameters
- 생성자의 파라미터를 받아서 클래스의 프로퍼티로 적용하는 방법
```ts
class Person {
  constructor(public name: string, private age: number) {
  }
}

const p1: Person = new Person("Mark", 39);
console.log(p1); 
```

## Getters & Setters
```ts
class Person {
  constructor(public _name: string, private age: number) {}

  get name() {
    //
    console.log("get");
    return this._name;
  }

  set name(n: string) {
    console.log("set");
    this._name = n;
  }

}

const p1: Person = new Person("Mark", 39);
console.log(p1.name); //get을 하는 함수 getter
p1.name = "jonadan"; // set을 하는 함수 setter
```

## readonly properties
- readonly 는 초기화되는 영역에서만 할당가능하며 다른 곳에서는 값을 바꿀수 없다.
```ts
class Person {
  public readonly name: string = "Mark";
  private readonly country: string;
  public constructor(public _name: string, private age: number) {
    this.country = "korea"; //여기서랑 위에 선언할때 가능 밑에서는 불가능
  }

  hello() {
    this.country = 'China'; // 여기 에러
  }

}
```

## Index Signatures in class
```ts
// class => object
// {mark: 'male', jade: 'male'}
// {chloe: 'femail', alex: 'maile', anna: 'female'}

class Students {
  [index: string]: "male" | "female";

  mark: "male" = "male";
}

const a = new Students();
a.mark = "male";
a.jade = "male";

console.log(a);

const b = new Students();
b.chloe = "female";
b.alex = "male";
b.anna = "female";
```

## static properties & methods
```ts
class Person {
  public static CITY = "seoul";
  public hello() {
    console.log("안녕하세요");
  }
  public change() {
    Person.CITY = "LA";
  }
}

const p1 = new Person();
p1.hello();
// p1.hello(); // 스테틱을 쓰면 에러 안쓰면 가능

const p2 = new Person();
p2.hello();
// Person.hello(); // 스테틱 쓰면 가능 안쓰면 에러
p2.change();
p2.hello();
```

## Singletons
```ts
class ClassName {
  private static instance: ClassName | null = null;
  public static getInstance(): ClassName {
    // ClassName 으로부터 만든 object가 있으면 그걸 리턴
    // 없으면, 만들어서 리턴
    if (ClassName.instance == null) {
      ClassName.instance = new ClassName();
    }

    return ClassName.instance;
  }

  private constructor() {}
}

const a = ClassName.getInstance();
const b = ClassName.getInstance();

console.log(a == b);
```

## 상속(Inheritance)

```ts
class Parent {
  constructor(protected _name: string, private _age: number) {}

  public print(): void {
    console.log(`이름은 ${this._name} 이고, 나이는 ${this._age}입니다.`);
  }

  protected printName(): void {
    console.log(this._name, this._age);
  }
  
}

// const p = new Parent("Mark", 39);
// p.print();

class Child extends Parent {
  public _name = 'Mark Jr.';
  
  public gender = 'male';

  constructor(age: number) {
    super('Mark Jr.',age) // 이걸 먼저 써야 오류가 안난다.
    this.printName();
  }
}

const c = new Child(1);
c.print();  
```
## Abstract Classes
```ts
abstract class AbstractPerson {
  protected _name: string = 'Mark';

  abstract setName(name: string): void;
}

// new AbstractPerson()

class Person extends AbstractPerson{
  setName(name: string): void {
    this._name = name;
  }

}

const p = new Person();
p.setName();  // 에러
```

## Generics, Any와 다른점
 ```ts
 function helloString(message: string): string {
  return message;
}
function helloNumber(message: number): number {
  return message;
}
function hello(message: any): any {
  return message;
}
console.log(hello("Mark"));
console.log(hello(39). length);

function helloGeneric<T>(message: T): T {
  return message;
}
console.log(helloGeneric('Mark').length);
console.log(helloGeneric(39));
console.log(helloGeneric(true));
```

## Generics Basic
- 타입을 지정하면 지정된 타입으로 규정이되고 그렇지 않으면 추론에 의해 타입이 정해진다.
```ts
function helloBasic<T, U>(message: T, comment: U): T {
  return message;
}
helloBasic<string, number>("Mark", 39); //string타입으로 규정
helloBasic(36, 39); // 추론에의해서 타입이 정해짐
```

## Generics Array & Tuple
```ts
/*array 형태*/
function helloArray<T>(message: T[]): T {
  return message[0];
}

helloArray(["hello", "world"]);
helloArray(["Hello", 5]);
/*tuple 형태*/
function helloTuple<T, K>(message: [T, K]): T {
  return message[0];
}
helloTuple(["Hello", "World"]);
helloTuple(["Hello", 5]);

```
## Generics Function
- 함수의 타입만 선언하는 방식
```ts
type HelloFunctionGeneric1 = <T>(message: T) => T;

const helloFunction1: HelloFunctionGeneric1 = <T>(message: T): T => {
  return message;
};

interface HelloFunctionGeneric2 {
  <T>(message: T): T;
}

const helloFunction2: HelloFunctionGeneric2 = <T>(message: T): T => {
  return message;
};
```

## Generics Class
```ts
class Person<T, K> {
  private _name: T;
  private _age: K;

  constructor(name: T, age: K) {
    this._name = name;
    this._age = age;
  }
}
new Person("Mark", 39);
//new Person<string>(39); //string 타입인데 숫자가 들어갔으므로 에러
new Person<string, number>("Mark", "age");  // age 는 에러
```

## Generics with extends
```ts
class PersonExtends<T extends string | number> {
  private _name: T;
  
  constructor(name: T){
    this._name = name;
  }
}

new PersonExtends("Mark");
new PersonExtends(39);
new PersonExtends(true);  // true는 에러
```

## keyof & type lookup system
```ts
interface IPerson {
  name: string;
  age: number;
}
const person: IPerson = {
  name: "Mark",
  age: 39,
};


function getProp<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}
getProp(person, "age");

function setProp<T, K extends keyof T>(obj: T, key: K, value: T[K]): void{
  obj[key] = value;
}
setProp(person, "name", "Anna");
```