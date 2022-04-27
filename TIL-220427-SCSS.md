# SCSS

## 개요
- 기존의 CSS문법을 대체하기 위해 나왔다. SCSS,SASS가 있는데 여기서는 SCSS문법을 배울 것
- 새로운 문법이 나오게 된 이유는 순수한 CSS문법을 이용하면 불편할 수가 있는데 좀 더 편하게 하기 위해서 나오게 되었다.
- sass,scss문법으로 작성하면 바로 브라우저가 읽을 수 없기 때문에 css문법으로 바꿔주는 컴파일이 이루어져야 한다.
- 다른 대체 문법인 less, stylus가 있지만 조금 더 안정적이고 사람들이 많이 사용하는 sass를 배울 것이다.
- SASSMEISTER.COM 에서 scss문법이 css 로 어떻게 바뀌는지 한번에 확인할 수 있다.

## 주석
- 컴파일 후에도 주석처리를 남기려면 /* */를 이용하고 그렇지 않다면 // 를 써도 된다.

## 중첩 with SassMeiset
- 밑의 예제처럼 한번에 중첩시켜서 사용할 수 있다. 자식요소를 선택하고 싶을 때에는 > 를 사용하면 된다.
```css
.container {
  ul {  //여기 ul앞에다가 > 를 넣어서 사용가능하다.
    li {
      .name {
        .color: royalblue;
      }
      .age {
        .color: orange;
      }
    }
  }
}
```

## 상위(부모)선택자 참조
- &를 이용해서 상위(부모)를 선택할 수 있다.
```css
.btn {
  &.active{   // 여기서 &는 부모인 btn을 의미한다.
    color: red;
  }
}
```
## 중첩된 속성
- 반복적으로 이용되는 속성을 편하게 사용할 수 있는 방법
```css
.box {
  font: {
    weight: bold;
    size: 10px;
    family: sans-serif;
  };  // ;을 붙여줘야 한다.
}
```

## 변수
- js나 c언어에서 변수를 선언하는것처럼 변수를 $를 이용해서 변수를 선언할 수 있다.
```css
$size: 200px;
```
- 변수의 유효범위가 있다. 그 범위는 변수가 선언된 중괄호 안에서만 유효하다.
- 같은 변수가 재할당되면 재할당된 값으로 사용된다.

## 산술 연산
- 일반적인 연산자를 사용할 수 있다. 하지만 나눗셈 `/` 기호는 정상적으로 작동되지 않는다.
- 나눗셈을 사용하기 위해서는 소괄호로 닫아서 사용하거나 변수를 이용하거나 다른 연산자와 함께 사용하면 된다.
- 연산하는 단위가 서로 같아야한다. 다른 경우에는 calc()를 이용하자.
```css
margin: (10px / 2); //소괄호 이용하면 나눗셈 사용 가능
margin: $size / 2;  //변수를 이용하면 나눗셈 사용 가능
margin: 5 + 10px / 2; // 다른 연산자와 함께하면 나눗셈 사용 가능
```
## 재활용(Mixins)
- @mixin 을 이용해서 코드를 작성하면 @include를 이용해 재활용할 수 있다.
```css
@mixin box {
  widht: 100px;
  height: 100px;
  background-color: black;
}
.container {
  @include box;
}
```css
@mixin box($size) { //이런식으로 매개변수를 이용도 가능하다.
  widht: $size;
  height: $size;
  background-color: black;
}
.container {
  @include box(200px);
}
```
```css
@mixin box($size: 100px) { //뒤에서 재활용할 때 인수를 넣지않으면 100px으로 할당된다.
  widht: $size;
  height: $size;
  background-color: black;
}
.container {
  @include box(200px);
}
```
```css
@mixin box($size: 100px, &color: black) { //이렇게 두개도 가능하다.
  widht: $size;
  height: $size;
  background-color: $color;
}
.container {
  @include box(&color: red);  //사이즈의 기본값인 100px를 건드리지 않으려면 이렇게 아니면 (50px, red) 이런식으로 넣으면 된다.
}
```

## 반복문
```css
@for $i from 1 through 10 { // i라는 변수가 1부터 10이 될 때까지 반복
  .box:nth-child(#{$i}) { //()안에 숫자가 들어가야하는데 $i를 그대로 넣을 수 없어서 보간을 이용하여 넣는다.
    width: 100px;
  }
}
```

## 함수
- js처럼 @function 을 통해 함수와 비슷한 기능을 제공한다.
```css
@function ratio($size, $ratio) {
  @return $size * $ratio
}
.box {
  $width: 100px;
  width: $width;
  height: ratio($width, 1/2); // height에 50px가 적용이 된다.
}
```

## 색상 내장 함수
- 색상관련해서 내장되어있는 함수
```css
background-color: mix(red, blue); // 둘을 섞는다
background-color: lighten(red, 10%);  // 10%만큼 밝게
background-color: darken(red, 10%); // 10만큼 어둡게
background-color: saturate(red, 30%); // 30%만큼 채도를 높게
background-color: desaturate(red, 30%); // 30%만큼 채도를 낮게
background-color: grayscale(red); // 회색화
background-color: invert(red);  // 색반전
background-color: rgba(red, .5);  // 투명화, .5 이므로 50%만큼
```

## 가져오기
- css에서 @import를 통해 다른 css파일을 가져올 수 있었던 것처럼 scss에서도 그 기능을 제공한다.
- css랑 다르게 `@import "./sub";` 이런식으로 뒤에 확장자명을 생략할 수 있다.

## 데이터 종류
- $number, $string, $color, $boolean, $null, $list, $map
```css
$map: ( // 객체데이터와 비슷하다.
  o: orange,
  r: royalblue
);
```
## 반복문 @each
```css
@each $c in $list { //리스트에있는 데이터들을 반복해서 변수c에 넣으면서 밑의 문구를 실행한다는 뜻.
  .box {
    color: $c;
  }
}
```
- `$c`, 부분을 `$c, $d` 로 해서 사용도 가능하다. 뜻은 리스트에있는 데이터들을 각 두 변수에 넣으면서 밑의 문구를 실행. 

## 재활용 @content
- @content를 이용해 재활용코드에 내용을 추가해서 사용할 수 있다.
```css
@mixin left-top {
  position: absolute;
  top:0;
  @content;
}
.box {
  width: 200px;
  @include left-top {
    bottom:0;
    right:0;
    margin: auto;
  }
}
```
- 이런식으로 위에서 이미 작성되어있는 positon, top 내용 이외에 bottom, right, margin에 대한 내용을 추가 가능하다.