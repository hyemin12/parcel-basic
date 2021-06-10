# Bundler

## parcel bundler 
구성 없는 단순한 자동 번들링  
소/중형 프로젝트의 적합  

## 정적파일 연결
```dash
$npm i -D parcel-plugin-static-files-copy

*package.json 파일에 작성
"staticFiles": {
    "staticPath": "static"
  }
```

## 공급 업체 접두사 적용하는 패키지
browserslist 옵션은 현재 NPM 프로젝트에서 지원할 브라우저의 범위를 명시하는 용도
그 명시를 autoprefixer 패키지가 활용함

1. $npm i -D postcss autoprefixer

2. package.json 파일에 작성
```json
"browerslist": [
    "> 1%",
    "last 2 versions" //전세계 점유율이 1%이상인 모든 브라우저, 그리고 2개 버전까지는 지원
  ]
```
3. .postcssrc.js 파일 생성

4. 코드 작성
```js
  module.exports = {
  plugins: [
    require('autoprefixer')
  ]
}
```
* 확인하려면 display:flex 입력 후 개발자모드 들어가서 확인
* 오류 날 경우 npm i autoprefixer@9  
  (autoprefixer10버전과 PostCSS 8과는 충돌이 많이 일어나서 autoprefixer9버전 설치하는 것을 권장  
  PostCSS plugin autoprefixer requires PostCSS 8.)

## babel
ECMAScript2015이전의 코드를 이전 자바스크립트 엔진에서 실행할 수 있는 이전버전과 호환하는 버전으로 변환해주는 컴파일러

1. npm i -D @babel/core @babel/preset-env

2. .babelrc.js 파일 생성

3. 코드 작성
```js
  module.exports = {
    presets: ['@babel/preset-env']
  }
```

* 정상적인 동작 확인
1. main.js 파일에 작성
```js
async function test() { //비동기 함수
  const promise = Promise.resolve(123)
  console.log(await promise)
}
test()
```

2. npm i -D @babel/plugin-transform-runtime

3. 코드 추가
```js
  module.exports = {
    presets: ['@babel/preset-env'],
    plugins: [
      ['@babel/plugin-transform-runtime']
    ]
  }
```

## 커맨드 라인 인터페이스(CLI)

* 명령어
  - Serve 개발용 서버 시작
   [parcel index.html]
  - Build 실제로 제품화 
   [parcel build index.html]
* 옵션
- 결과물 디렉토리  
    기본값 dist
  - 다른 폴더명을 사용할 때
  [parcel build index.html --out-dir 폴더루트]
- 포트번호
   기본값 1234
  - 포트 번호 변경
  [parcel serve index.html --port 변경원하는번호]
- 브라우저 열기
  기본값 false
  - 개발 서버 열 때마다 브라우저 열기
  [parcel index.html --open]
- 빠른 모듈 교체(HMR)
  런타임에 페이지 새로고침 없이 수정된 내용을 자동으로 갱신하는 방식
  - 비활성화 하는 방법
  [parcel index.html --no--hmr]

## 브라우저, node.js에서의 가져오기/내보내기

```js
***ESM - 브라우저에서 동작
***CommonJS - node.js에서 동작

// import - 브라우저에서 동작
// require() - node.js에서 동작

import autoprefixer from 'autoprefixer'
const autoprefixer = require('autoprefixer')

// export - 브라우저에서 동작
// module.exports - node.js에서 동작

export {
  plugins: [
    autoprefixer
  ]
// }
module.exports = {
  plugins: [
    autoprefixer
  ]
}
```





## Webpack bundler
매우 꼼꼼한 구성
중/대형 프로젝트에 적합


*** favicon 만들기
https://www.icoconverter.com/