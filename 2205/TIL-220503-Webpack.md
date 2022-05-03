# Part 8 .Bundler
# Webpack

## 프로젝트 생성
- 프로젝트 생성후 터미널을 열어서 다음 명령어를 쳐서 세팅을 해준다.
`npm init -y`
`npm i -D webpack webpack-cli webpack-dev-server@next` - @next는 서로 버전을 일치시키기 위해
- package.json 파일로 가서 script란에 test를 지우고 아래를 입력한다.
```
    "dev": "webpack-dev-server --mode development", // 개발모드
    "build": "webpack --mode production"  // 제품모드
```
- webpack.config.js: 부속옵션을 제공해줄 수 있는 파일이다.

## entry, output, plugins
```js
const path = require('path')
const HtmlPlugin = require('html-webpack-plugin')

require('path') // node.js에서 사용할 수 있는 전역 모듈

module.exports = {
  // 파일을 읽어들이기 시작하는 진입점 설정
  entry: './js/main.js',  //진입을 이 파일로 하겠다.

  //결과물(번들)을 반환하는 설정, path에는 절대경로를 입력해야한다.
  output: {
 //   path: path.resolve(__dirname, 'dist'),//resolve: 두 인수를 합쳐주는 역할, __dirname: 현재파일이 있는 경로를 지칭한다. node.js에서 사용할 수 있는 전역 변수임.
 //   filename: 'main.js',  // 위 두 부분이 디폴트 값이라서 지워도 똑같이 기능한다.
    clean: true // 새로 빌드명령을 돌렸을 때 기존에 있던 파일을 지워주는 기능.

  },
  // 번들링 후 결과물의 처리방식등 다양한 프러그인들을 설정
  plugins: [
    new HtmlPlugin({
      template: './index.html'
    })
  ],

  devServer: {
    host: 'localhost' // 이거 없이 하면 주소가 [::]8080이런식으로 뜨는데 하면 http://localhost:8080/이런식으로 다시 나온다.
  }
}  
```

## NPX, Degit
- `npx degit` 명령어를 이용하면 버전관리를 하지 않는 상태로 다운로드 받을 수 있다.
- `npx degit joseph-wee/joseph-wee.github.io test`
- `npx degit 깃허브리파지토리제목 다운받을폴더이름`