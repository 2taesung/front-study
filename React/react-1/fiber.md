# Fiber

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

실제 구현 코드에는 'work' 라는 키워드로 들어가 있다.



### Fiber가 무엇이냐?

Dom에 element가 있다면 React에서 효율성, 기능성을 위해 16버전부터 적용한 Fiber node이다.

기본적으로 React의 렌더링 효율성을 큰 폭으로 증가시켰고&#x20;

React 전체 구조가 렌더링 되는것보다 Fiber node 덕분에 node 별로 렌더링이 가능하다.



### Fibers are often created from React elements&#x20;

Fibers는 React elements에서 생기고 이 둘은 상당히 비슷간 개념을 공유합니다.

React elements와 type, key property를 공유합니다.



React elements는 렌더링마다 새로 생기지만&#x20;

대부분 Fiber는 초기 마운트 시 생성되고 가능한 한 재사용됩니다.



Fiber의 특징

* Fiber는 항상 '어떤 것(instance, DOM node ...)'과 1대1 관계를 갖습니다.
* "어떤"의 유형은 0\~24까지의 tag property 번호 내에 저장
* <mark style="background-color:orange;">stateNode ??</mark>

the stateNode property holds the reference React can access the state associated with the Fiber.



* child, sibling, return (Fiber relationShips)
* Fibers 도 tree 구조
* single child는 first child를 참조

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>



Work

* state change -> work
* lifeCycle function -> work
* changes in the DOM -> work



구체적   Work 가 할 수 있는건 ?

* work는 직접, 예약해서 사용할 수 있음
* time slicing을 사용하여 work 는 chunk들로 쪼갤 수 있음
* 애니메이션 같은 우선순위 높은 work는 가능한 빠르게 작동할 수 있
* 이와 함께 낮은 우선순위를 가진 work의 작업은 연기.

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

* React work는 비동기 render phase 과정에서 비동기로 작업하며 commit phase에서도 작동한다.
* What type of work? Lifecycle methods / DOM changes&#x20;



work의 효과는?

* &#x20;DOM 변환/ 특정  lifecycle method를 요청함
* Home component(div) -> updating the DOM
* Effects는 firstEffect, lastEffect, nextEffect, etc 과 같은 속성을 사용하여 추적됨.
*



[https://simsimjae.tistory.com/472](https://simsimjae.tistory.com/472)

[https://pshdev1030.github.io/2021/12/31/React-fiber/](https://pshdev1030.github.io/2021/12/31/React-fiber/)

[https://www.youtube.com/watch?v=0ympFIwQFJw](https://www.youtube.com/watch?v=0ympFIwQFJw)

[https://ichi.pro/ko/inside-fiber-reactui-saeloun-jojeong-algolijeum-e-daehan-simcheungjeog-gaeyo-248215941214062](https://ichi.pro/ko/inside-fiber-reactui-saeloun-jojeong-algolijeum-e-daehan-simcheungjeog-gaeyo-248215941214062)



<figure><img src="../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

