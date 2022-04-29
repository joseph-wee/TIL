## 정규표현식을 다루는 메소드

### test
- 일치 여부(Boolean) 반환
- `정규식.test(문자열)`
### match
- 일치하는 문자열의 배열 반환
- `문자열.match(정규식)`
### replace
- 일치하는 문자열을 대체하고 대체된 문자열을 반환
- `문자열.replace(정규식, 대체문자)`

## 플래그(옵션)

플래그 | 설명
--|--
g | 모든 문자 일치하는지(global)
i | 영어 대소문자를 구분하지 않고 일치하는지(ignore case)
m | 여러 줄 일치(multi line)

```js
const str = ` 
010-1234-5678
joseph@gmail.com
https://www.omdbapi.com/?apikey=7035c60c&s=frozen
The quick brown fox jumps over the lazy dog
abbaaccdddd
`

const regexp = /the/g // /the/gi 
console.log(str.match(regexp))

// const regexep = /the/gi  도 가능
```
- `\` : 이스케이프 문자로 본래의 기능에서 벗어나 다른식으로 해석될 수 있게 해주는 것 ex)`\.` .의 본래 기능인 찾는 역할이 아닌 문자열. 로 쓰인다. 
```js
console.log(str.match(/\./gi))  //문자열 . 와 일치하는 배열 반환
```
- `$` : 문장의 끝나는 부분에서 검사
```js
console.log(str.match/\.$/gim)  //문장의 끝이 . 로 끝나는 배열 반환 gim은 엔터친거를 인식해서 각 문장마다 검사
```
## 패턴(표현)
패턴 | 설명
--|--
^ab | 줄 시작에 있는 ab와 일치
ab$ | 줄 끝에 있는 ab와 일치
. | 임의의 한 문자와 일치
a&verbarb | a 또는 b 와 일치
ab? | b가 없거나 b와 일치
{3} | 3개 연속 일치
{3,} | 3개 이상 연속 일치
{3,5} | 3개 이상 5개이하 연속 일치
[abc] | a 또는 b 또는 c
[a-z] | a부터 z사이의 문자 구간에 일치(영어 소문자)
[A-Z] | A부터 Z사이의 문자 구간에 일치(영어 대문자)
[0-9] | 0부터 9사이의 숫자 구간에 일치
[가-힣] | 가부터 힣사이의 문자 구간에 일치
\w | 63개 answk(Word, 대소영문 52개 + 숫자10개 + _)에 일치
\b | 63개 문자에 일치 하지 않는 문자 경계
\d | 숫자에 일치
\s | 공백(Space, Tab 등)에 일치
(?=) | 앞쪽 일치
(?<=) | 뒤쪽 일치

```js
console.log(
  str.match(/^t/gim)  // 모든 줄의 앞부분에서 t와 일치한지 검사
)
console.log(
  str.match(/h..p/gi)  // . 사용법
)
console.log(
  str.match(/fox|dog/gi)  // fox 또는 dog 찾음
)
console.log(
  str.match(/https?/gim) // https 에서 s는 있든 없든 일치한걸 찾음 
)
console.log(
  str.match(/d{2}/g)  // 문자 d가 두번연속 일치하는지 즉, dd와 일치한 부분을 찾는다.  
)
console.log(
  str.match(/d{2,3}/g)  // 문자 d가 2번 혹은 3번 연속 일치하는지, 즉 dd, ddd와 일치한 부분을 찾는다.  
)
console.log(
  str.match(/\bf\w{1,}\b/g) // f로 시작하는 단어를 찾는다.  
)
console.log(
  str.match(/(?<=@).{1,}/g) // @뒤의 임의의 문자와 일치한지 검사후(. 이므로 무조건 일치) 연속된 모든 문자를 찾는다.  
)
```


***
### 기타
