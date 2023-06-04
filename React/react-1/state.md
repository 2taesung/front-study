# state

### 리액트에서 리렌더링이 되는 시점.

<mark style="color:red;">리액트에서 state를 사용하는 이유는 UI와 상태(state)를 연동시키기 위해서입니다.</mark>&#x20;

\=> 잘못된말 연동은 그냥 변수로도 됨.

근본적으로 UI는 어떠한 데이터가 있고 그것을 보기 편한 형태로 표현한 것입니다. 리액트는 이를 이해하고 UI와 연동되어야 하고, <mark style="color:green;">변할 여지가 있는 데이터들을 state</mark>라는 형태로 사용할 수 있게 해주었습니다. 그리고 데이터가 변경되었을 때 UI가 그에 맞춰서 변화하기 위해서 <mark style="color:green;">state를 변경시키는 방법을 제한</mark>시키고(setState), <mark style="color:green;">이 함수가 호출 될 때 마다 리렌더링</mark>이 되도록 설계하였습니다.



\=> state는 rendering과 관련해 react hook를 이용해 react 생명주기 매서드들을 다루려고 만드는 거다.

\=> 실제로 state는 없이 만들수도 있다.

\=> 실제 예시를 들면 state로 isModal을 많이 쓰지

\=> 이거 같은 경우는 isModal 데이터가 변경되면 다시 렌더링을 시켜서 UI를 이에 맞게 바꿔줄 필요가 있다.



### state의 필요성&#x20;

1. 렌더링이 안돼서 화면에 반영이 안되어있더라도 데이터는 실제로 변화한다.

\=> 한마디로 일반 변수는 데이터가 바뀌더라도 바로 UI에 적용되지 않는다.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

2. rendering시 데이터가 보존되지 않는다. 렌더링이 되면 당연히 변수도 초기 할당값으로 재할당된다.

\=> state는 데이터가 변경이 되면 렌더링이 일어나더라도 데이터를 보존해주는 기능도 한다.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>









