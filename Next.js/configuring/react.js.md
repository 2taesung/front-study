# React.js와 비교해 주의해야할 점

많은 사람들이 CNA을 사용하는 것에 거부감이 없음

(CRA와 다르게)

그 이유는 무엇일까 ?



Next.js는 철학과 같이 React에서 설정으로 인한 불편함을 극도로 개선함.

또한 공식문서의 install을 가도  메뉴얼 설치와 CNA를 통한 설치, 솔직히 거의 차이가 없다.

왜냐하면 React와 달리 기타 react-router-dom 과 같은 추가적인 라이브러리 설치가 필요 없기 때문.

그렇기 때문에 더 명확하다.

Next.js를 사용하는 자체가 CRA를 통해 했던 것들을 이미 한번 개선해서 추상화 한 프레임워크이기 때문일것.

\=> 고로 production도CNA를 해도 상관 없다고 판단.



관련 단테님의 의견

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>



* Routing 방식의 차이 react-route-dom 노app route 시스템 고
* CSS and Sass, stylede-component 같은 애들 추가로 설치할 필요 없음
* 자동으로 image 관련 최적화 해줌.



### default 값이 server side

ssr 페이지나 정적으로 생성된 페이지 모두 Node.js에서 실행되기 때문에 fetch, window, document와 같이 웹 브라우저에서 제공하는 전역 객체나 canvas 같은 HTML 요소에는 접근할 수 없음.



그래서 이를 다양한 방법들로 해결하려고 하고 있긴 한데.

가장 대표적인 방법은 해당 요소들의 사용을 브라우저에서 mounted가 된 이후로 미루는 것이다.

\=> 굉장히 아름답지 못하다.





### babel plugin

Next.js가 babel의 @babel/plugin-transform-typescript를 사용해 설정 파일을 관리

* const enum 지원 x
* export =와 import = 구문 사용 x





