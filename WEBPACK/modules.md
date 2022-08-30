## Modules

모듈러 프로그래밍에서는, 개발자들은 모듈이라고 불리는 하나의 기능 뭉치를 쪼갠다.

각각의 모듈들은 전체 프로그램에 비해서 작은 크기를 가지기 때문에 검증하고, 디버깅하고 테스팅하기에 쉽다. 잘 작성된 모듈은 견고한 추상화와 캡슐화의 경계를 제공하는데, 그렇게 함으로써 각각의 모듈들은 응집력있고 더 분명한 목적을 가지게 된다.

노드는 초기부터 모듈러 프로그래밍을 지원해왔지만, 브라우저는 그렇지 않았다. 브라우저는 모듈이 도착하는데에 느린 환경을 제공했엇다.  
자바스크립트 모듈을 웹에서 지원하기 위한 다양한 도구들이 존재했다. 다양한 이점과 한계점을 가지고서.  
웹팩은 이런 시스템들에거 얻은 교훈을 바탕으로 만들어졌으며, 프로젝트에 존재하는 모든 파일에 대해서 모듈의 개념을 적용한다.

## What is Webpack Module

노드에서의 모듈과 대조적으로, 웹팩에서는 모듈을 다양한 방식으로 표현할 수 있다.

- An ES2015 import statement
- A CommonJS require() statement
- An AMD define and require statement
- An @import statement inside of a css/sass/less file.
- An image url in a stylesheet url(...) or HTML <img src=...> file.
