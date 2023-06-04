# State

* “Step 3: Find the minimal but complete representation of UI state”
* “Step 4: Identify where your state should live”

useState로 대표되는 state 역시 React로 개발을 하는데 SRP와 양대산맥.

\=> 현재까지는 무지성으로 필요한 경우에 useState를 만들어썼다.

\=> 그러나 이제부터는 React 안의 다양한 도구들을 정확한 목적과 기능을 알고 적절한 판단(최적화)을 가지고 사용해야한다. 그래야 전문가가 될 수 있음.



### React의 state는 "변경"을 다루기 위한 요소.

"Re-rendering"이라는 주제에서 다뤄진다.



우리는 이 state를 일관성과 효율을 위해 DRY 원칙을 따르는 SSOT를 만든다.



### state는 비즈니스 로직과 유기적으로 연결된다.

쉽게 생각해서 state가 데이터랑 이꼴\*3(js이니까)  이라고 생각하면 그냥 막 만들면 됨.

그냥 변수 선언해서 가져다가 쓰면 됨.

{% hint style="info" %}
여기서 그냥 변수는 그러면 언제 쓰면 되는가?

변하지 않고 state 상태값에서 부가적으로 생성되는 데이터들은 변수를 그냥 써서 유기적으로 state가 변경되면서 렌더링 한번으로 다같이 바꿔주는게 현명하고 중복 rendering이 발생하지 않는다.&#x20;



만약 state에서 파생되는 데이터를 또 state로 만들게 되면 연쇄적으로 렌더링이 수차례 반복하면서 점점 복잡하고 비효율적인 앱이 되어간다.

```javascript

const filters = filterText + filterCategory;

return (
  <p>
    <h1>{filters}</h1>
  ...
)
```
{% endhint %}



그런데 state 로 우리는 <mark style="background-color:red;">비즈니스 로직(핵심 데이터)가 변경되면 다같이 유기적으로 변경되는 아름다운 구조</mark>를 만드는게 목표.&#x20;

\=> 이 역시 state는 '변경'을 다루는 요소라는 것에 저절함.

\=> 아 ... 그래서 setState를 하면 전체  렌더링을 하네(React 개발한 사람이 이 부분을 고려했다는것)

\=> 왜? state는 '변경'을 다루는 요소니까



\=> 또한 우리의 비즈니스 로직에 관여된 데이터들은 빈번하게 변경이 됨.

\=> 댓글이 달린다거나, 게시물이 삭제된다거나 등등

\=> 이로 효율성 및 최적화를 가져올 수 있음&#x20;

\=> 실제로 내가 개발한 서비스는 sector를 추가할 때 거의 5군데를 일일히 찾아가서 수정해줘야함;;;; (창피하지만 리액트 처음 개발할때 만들어진...)



### DRY 원칙을 따르는 SSOT를 만든다.

* [DRY (Don’t Repeat Yourself)](https://ko.wikipedia.org/wiki/%EC%A4%91%EB%B3%B5%EB%B0%B0%EC%A0%9C)
* [SSOT (Single Source of Truth)](https://ko.wikipedia.org/wiki/%EB%8B%A8%EC%9D%BC\_%EC%A7%84%EC%8B%A4\_%EA%B3%B5%EA%B8%89%EC%9B%90)

<mark style="background-color:green;">위의 사례와도 연관이 되고 state를 기반으로 또 다른 state를 만드는 것 역시 지양해야함.</mark>

<mark style="background-color:green;">=> 이건 정확히 생각을 해보자 로직에 따라서는 빈번하게 state를 의존적으로 만들기는 하는것 같은데 또 이렇게 생각하면 불필요한 렌더링이 두배로 드는셈이니까</mark>&#x20;

<mark style="background-color:green;">=> React 개발할때 나오던 의존성 err가 혹시 이건가 ;; => 생각 및 질문하기</mark>

\=> 강의에서 나오는 '계산 가능한' 사례에 해당함. useEffect를 이렇게 쓰지마라.

[You Might Not Need an Effect](https://beta.reactjs.org/learn/you-might-not-need-an-effect)

\=>  공식문서에 있는 bad example이 ;;;

\=>  내가 실제 개발하면서 상당히 많이 사용하던 useEffect 사용 패턴 ;;;

\=> 다 없애야겠네... 잘못하고 있던 셈.

\=> 위의 공식 문서를 정독하고 공식 문서 가이드처럼 바꾸기. <mark style="background-color:red;">생각 및 습관조차.</mark>



최종적으로

> React State의 조건:
>
> 1. 변경돼야 함. 변경되지 않는 건 state로 다룰 가치가 없다.
> 2. 부모 컴포넌트가 props를 통해 전달한다면 state가 아님.
> 3. 다른 state나 props를 이용해 계산 가능하다면 state가 아님.



### State 관리에 TS 활용.

다루는 상태가 너무 많으면 복잡함.

TS를 잘 쓰면 직접 관리하는 상태의 수를 줄여줄 수 있다.

\=> 왜 ? JS에서는 데이터를 하나로 object로 묶어서 props를 내려주는 일들이 부담이 되고 걱정이 된다.

\=> 그래서 안전하게 데이터를 까서 props 해주는 게 옳은 방법일 수 있어

\=> 그러나 ts를 쓰면 propsType 만들기도 하니까 그러므로 위의 걱정 없이 데이터들을 묶어서 처리할 수 있게 됨.



\=> 이 도구(ts)가 있음으로 내게 선택권이 생긴다.

\=> state 데이터를 props로 내릴때 하나씩 특정해서 보낼지.

\=> 아니면 너무 복잡하고 수고스러우니 ts를 통해 object로 보낼지.



### Lifting State Up

그렇다면 특정 state 관리의 주체는 어느 컴포넌트(위치) 여야하냐

답은 최상위 컴포넌트. (더이상 필요치 않은)

* [“Lifting State Up”](https://ko.reactjs.org/docs/lifting-state-up.html)
* [Sharing State Between Components](https://beta.reactjs.org/learn/sharing-state-between-components)

\=> 기본적으로 state 지점을 찾는건 열심히 고민을 해서 가장 최상위 컴포넌트에서 시작하면서 개발하면 베스트.

\=> 그런데 개발하다보면 변경사항이 생길 수 밖에 없음.

\=> 그럴때는 하위 컴포넌트에서 상위 컴포넌트로 올려주면서 (lifting state up) 위치를 잡는 것도 한 방법.



{% hint style="info" %}
지금까지 한번도 생각해보지 못했었는데 함수를 props로 내려줄 수 있는 이유도 js 가 1급 객체이기 때문
{% endhint %}
