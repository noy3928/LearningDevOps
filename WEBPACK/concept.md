## Entry

엔트리포인트는 이것의 내부적인 의존성 그래프를 그리기 위해서 어디서부터 시작하면되는지를 알려준다.  
그리고 웹팩은 이 엔트리포인트가 의존하고 있는 다른 모듈과 라이브러리들을 알아낼 것이다.

기본적으로 이것의 값은 ./src/index.js이지만, 엔트리포인트를 설정함으로써 커스터마이징할 수 있다. 예를 들면

```javascript
//webpack.config.js
module.exports = {
  entry: "./path/to/my/entry/file.js",
}
```

<br>

## Output

ouput 속성을 통해서는 번들 결과물을 어디에 내보낼지, 그것의 이름은 무엇으로 정할지를 지정한다.  
이것의 메인 결과 파일은 기본적으로 ./dist/main.js 에 저장되고, ./dist 폴더에는 다른 생성된 파일들이 저장된다.

이것 또한 지정해줄 수 있다.

```javascript
//webpack.config.js
const path = require("path")

module.exports = {
  entry: "./path/to/my/entry/file.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "my-first-webpack.bundle.js",
  },
}
```

이 예제에서 output을 사용하고 있다. 이 안에서 파일의 이름과, 저장할 위치를 지정하고 있다.  
path 모듈에 대해서 궁금할 수 있는데, 이것은 file paths를 조작하기 위한 노드의 핵심 모듈이다.

<br>

## Loaders

기본적으로 웹팩은 자바스크립트와 json파일만 이해한다.  
loaders는 웹팩이 다른 종류의 파일들에 대해서도 작업을 진행하고, 그것들을 유효한 모듈로 변환할 수 있도록 해준다.  
그런 유효한 파일들을 통해서 어플에서 사용될 수 있고, 또 의존성 그래프에도 추가될 수 있다.

loaders는 2가지 기능을 제공한다.

1. test : 어떤 파일을 변환시켜야하는지를 선택한다.
2. use : 변환을 수행하는 데 사용할 로더를 나타낸다.

```javascript
//webpack.config.js
const path = require("path")

module.exports = {
  output: {
    filename: "my-first-webpack.bundle.js",
  },
  module: {
    rules: [{ test: /\.txt$/, use: "raw-loader" }],
  },
}
```

위 코드는 웹팩에게 다음과 같이 말하는 것이다.

> "Hey webpack compiler, when you come across a path that resolves to a '.txt' file inside of a require()/import statement, use the raw-loader to transform it before you add it to the bundle."

<br>

## Plugins

로더가 특정 모듈에 대한 변환을 위해서 사용된다면, plugins는 더 넓은 범위의 작업을 위해서 사용된다.  
예를 들면, 번들 최적화나 asset 관리나, 환경변수 주입과 같은 것들이다.

플러그인을 사용하기 위해서는, require문을 사용해야한다. 그리고 플러그인 배열에 그것을 넣어줘야 한다.  
대부분의 플러그인들은 옵션을 통해서 커스터마이징이 가능하다.  
환경에서 다른 목적들을 위해서 플러그인을 여러번 사용할 수 있기 때문에, 새로운 연산자로 그것의 인스턴스를 만들 필요가 있다.

```javascript
//webpack.config.js
const HtmlWebpackPlugin = require("html-webpack-plugin")
const webpack = require("webpack") //to access built-in plugins

module.exports = {
  module: {
    rules: [{ test: /\.txt$/, use: "raw-loader" }],
  },
  plugins: [new HtmlWebpackPlugin({ template: "./src/index.html" })],
}
```

<br>

## Mode

모드를 설정 해줆으로써, 각각의 환경에 맞는 최적화를 할 수 있다.  
기본설정은 production이다.

```javascript
//webpack.config.js
module.exports = {
  mode: "production",
}
```

<br>

## Browser Compatibility

Webpack supports all browsers that are ES5-compliant (IE8 and below are not supported). Webpack needs Promise for import() and require.ensure(). If you want to support older browsers, you will need to load a polyfill before using these expressions.
