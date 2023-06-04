# createRoot()

[https://dev.to/fromaline/reactdomcreateroot-reactdomrender-1jg6](https://dev.to/fromaline/reactdomcreateroot-reactdomrender-1jg6)

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

* container

DocumentFragment : html 문서의 일부여야한다, 부모가 없는 최상단에 있는 코드여야한다.

* Concurrent Mode

React 18은 동시 모드 API의 진입점으로 createRoot 함수를 도입했습니다. 이 함수는 동시 모드를 사용하여 렌더링되는 React 애플리케이션의 루트 엘리먼트를 생성하는 데 사용됩니다. createRoot 함수는 startTransition과 같이 React 18에 도입된 새로운 API를 사용하여 애플리케이션을 렌더링하는 데 사용할 수 있는 루트 객체를 반환합니다.

* RootOptions

createRoot 함수는 렌더링할 DOM 엘리먼트인 하나의 필수 인자만 받습니다. 이 함수는 렌더링 및 마운트 해제 메서드가 있는 RootType 객체를 반환합니다. createRoot 함수는 또한 수화와 관련된 선택적 RootOptions 인수를 받습니다. 앱이 React로 완전히 빌드되면 전체 앱에 대해 단일 루트가 생성됩니다. 새로운 루트 API는 새로운 React 18 기능의 진입점 역할을 하며 즉시 사용 가능한 향상된 기능을 제공합니다.



<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<mark style="background-color:orange;">??? 2.</mark>



<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>





[vs ReactDOM.render](https://dev.to/fromaline/reactdomcreateroot-reactdomrender-1jg6)





