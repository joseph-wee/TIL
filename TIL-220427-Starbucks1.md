# 스타벅스 웹페이지 만들기

## 도움되는 사이트
- 구글에서 제공하는 아이콘 사이트: https://material.io/design/iconography/system-icons.html
- scss로 작성한코드를 변환에서 보여주는 사이트: https://www.sassmeister.com/

## 이미지
- 이미지 밑에 살짝 공간이 있는 이유는 이미지가 인라인요소이고 인라인요소는 글자처럼 취급되는데 글자가 차지하고 있는 공간의 높이는 글자크기가 아닌 글자의 em박스, line-height이기 때문이다.

## 아이템 중앙으로 배치하기
- 자식요소를 부모요소안에서 수직적으로 중앙에 배치하기 위해서는 자식요소에 이런식으로 넣어야한다.
```css
.container {
  position: relative;
}
.item {
  height: 100px;
  position: absolute;
  top: 0;
  bottom: 0;
  margin: auto 0;
}
```
- `top` `bottom` 값으로 0을 주는이유는 부모요소 제일 위쪽과 제일 아래쪽으로 부터 `margin: auto` 를 이용해 자동으로 위,아래 여백을 똑같이 주기 위해서이다. 또한 이를 계산하기 위해서 `height` 값이 명시되어있어야 한다.
- 자식요소에만 `position: absolute` 주고 끝이 아니고 부모에게 `position: relative` 을 명시해주어야 한다. 
- 만약 수직의 중앙이아닌 가로의 중앙에 배치하고 싶다면 위와 원리는 똑같이 가로 값들을 수정하면 된다.

## BEM(Block Element Modifier)
- HTML 클래스 속성의 작명법
- 요소__일부분 ex) `class="container__name"`
- 요소--상태  ex) `class="btn btn--primary"`

## 기타
- `cursor: pointer` - 커서의 모양을 바꿈  