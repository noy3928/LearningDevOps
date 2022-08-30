```javascript
const path = require("path")

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "dist"),
  },
}
```

웹팩 설정을 할 때 import문을 사용하지 않는 이유는,
웹팩 단계에서는 노드를 사용하기 때문에, import를 읽을 수가 없기 때문이다.

### 웹팩 script 실행

```
"build": "webpack --config webpack.config.js --mode development"
```

script 부분에 다음과 같이 적어줘야한다.  
webpack --config 다음에 파일명.

그리고 이렇게 생성한 파일을 index.html에 넣어준다.

```html
<button id="button1" onclick="sum(1,2)">Click me</button>
...
<script src="../dist/bundle.js"></script>
```

그런데 그냥 사용한 경우에 자바스크립트에서 사용하려했던 함수를 사용할 수가 없다.
왜 그런걸까??

```javascript
;(() => {
  function sum(a, b) {
    console.log(a + b)
  }
})()
```

이렇게 사용하는 것을 모듈패턴이라하는데, 이렇게 사용할 경우 스코프가 독립적으로 구분된다.
웹팩 파일도 빌드할 경우 번들 파일이 만들어지는데, 그 내부가 이렇게 생성되는 것을 확인할 수 있다.
때문에 이 자바스크립트 파일이 로드된다 할지라도, 독립적인 스코프를 내부적으로 가지고 있기 때문에,  
sum을 찾을 수 없는 것이다.  
이런 문제를 해결하기 위한 방법으로는 dom을 사용해 리스너를 등록하는 방법이 있다.

```javascript
document.getElementById("button1").addEventListener("click", function () {
  const el = document.getElementById("header")
  el.innerHTML = "Hey i have updated the code !"

  const listItems = ["Apple", "orange", "Banana"]
  const ul = document.getElementById("shoppingList")
  _.forEach(listItems, function (item) {
    const tempEl = document.createElement("li")
    tempEl.innerHTML = item
    ul.appendChild(tempEl)
  })
})
```

이렇게 한 경우에는 문제없이 버튼을 눌렀을 때 동작한다.
