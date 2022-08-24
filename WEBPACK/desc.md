# why?

어플리케이션을 브라우저에 가져와서 보여주려하는데,  
파일이 너무 많은 경우 네트워크에 무리가 간다.

그런 문제를 해결하기 위해서 하나의 파일에 다 담아서 브라우저에 보냈는데,
또 다른 문제가 있었으니, 디버깅하기가 힘들다는 것이고,  
scope조정하는 것이 쉽지 않다는 것이다.  
이런 문제를 해결하기 위해서 웹팩이 나왔다.

## 웹팩이 나와서 하는 일 :

1.다양한 종류의 asset 모듈을 Load할 수 있다.  
2.dependencies graph를 동적으로 만들 수 있다. 어떤것이 지금 필요하고, 필요하지 않은 지를 체크해서 만들 수 있다.  
3.라이브러리에서 코드를 지우는 것.  
4.반복된 코드를 지워주는 것  
5.런타임에 모듈을 fetching해주는 것.

## dependency graph :

가장 먼저 entry file이 존재해야한다.  
그 entry file을 통해서 다른 모든 모듈들이 연결될 것이다.  
만약 index.js 에서 cart.js의 코드를 import해오고 잇었다면,  
webpack은 cart.js 모듈을 로드할 것이다.  
그리고 cart.js가 내부적으로 order.js파일을 import하고 있다면,  
order.js 파일을 로드할 것이다. 이런식으로 쭉쭉 연결된 모듈들, asset들을 로드한다.

그리고 만약 아무도 참조하지 않는 모듈이 있다면,  
그 모듈은 지우고 올린다.

최종 결과물은 bundle.js, vendor.js, buncle.css에 담기게 될 것이고,  
결국에 index.html에는 해당 파일들을 참조하도록 만들기만하면 되는 것이다.