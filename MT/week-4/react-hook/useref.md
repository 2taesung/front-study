# useRef

[beta 문서의 useRef](https://beta.reactjs.org/reference/react/useRef)



주요 용도:

1. 컴포넌트가 사라질 때까지 동일한 값을 써야 하는 경우

\=> input 등의 ID 속성 관리

\=> 한 컴포넌트 내에서 여러개의 input 을 id로 특정해 활용 가능할 듯.



1. 주로 dom을 특정할 때 사용.

\=> 이 또한 한 컴포넌트 내에서 바뀌지 않는 경우에 해당하기도 한다.

\=> 내가 실제로 실무에서 chart(canvas) 객체를 유지할때 사용했음



3. (특히 useEffect 등과 함께 쓰면서 만나게 되는) 비동기 상황에서 현재 값을 제대로 쓰고 싶은 경우.

&#x20;\=> 이거 나 뭔지 안다. 나를 엄청 괴롭혔던 에러&#x20;

\=> prev를 쓰면 해결되기도 하는데 이건 또 set 함수 안에서만 인자로 가능한 기능.

\=> 이걸 해결하기 위해 useRef를 쓰는 방법을 찾기도 했음

\=> 이 현상을 표현 하기를 <mark style="background-color:red;">'Closure로 인한 변수를 capture, bind를 깜빡하는 문제'</mark>

\=> 해당 내용 정확히 공부해놓자.

\=> React 에서 가장 큰 문제 상황임.

{% hint style="info" %}
그냥 일반 변수 (예를들어, state 조합으로 파생 변수)와 역할을 구분해서 잘 쓸 것.
{% endhint %}



대표적인 예시,

내가 원하는건 5초 후의 filterText의 값인데

바로 렌더링 됐을 때 0초 후의 filterText 값이 capture 되기 때문에&#x20;

아무리 아래의 setTimeout을 해줬더라도 0초의 filterText 값이 출력된다.

```javascript
useEffect(() => {
	setTimeout(() => {
		console.log(filterText);
	}, 5_000);
}, []);
```
