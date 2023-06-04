# useEffect

[https://beta.reactjs.org/learn/synchronizing-with-effects](https://beta.reactjs.org/learn/synchronizing-with-effects)

> Some components need to synchronize with external systems.

synchronize라 함은 컴포넌트 외부와 동기시킨다.&#x20;

즉, 컴포넌트 외부에서 영향을 받는 것을 뜻 함.

예를 들면 props의 변화, axios를 통해 외부에서 들어오는 데이터.



되도록이면 useEffect를 쓰지마라(useEffect를 쓰는 상황을 강조하려함)

[You Might Not Need an Effect](https://beta.reactjs.org/learn/you-might-not-need-an-effect)

내가 생각했을때도 이름이 sideEffect 처럼 부작용의 의미도 useEffect에는 포함되어 있다.

왜냐하면 함수형 프로그래밍, 함수 단위의 유닛테스트 생각했을 때 함수의 input과 output에 집중을 하니까 return (output)으로 의미 있는 가치를 만들지 않는 useEffect 같은 경우는 함수형 프로그래밍의 철학에 어긋나는 셈이니까.



> 렌더링 이후 해야 할 일, 즉 React의 외부와 관련된 일을 정해줄 수 있다.
>
> 기본적으로 두번째 인자로 타이밍을 잡아주지 않는다면 렌더링시 항상 실행된다.
>
> 렌더링시에는 당연 state가 변경될때도 포함한다.

<mark style="background-color:orange;">예를 들어, DOM으로 떨어졌을때 그것을 잡기 위해 사용하기도 함 ???</mark>



```javascript
useEffect(() => {
    document.title = `Now: ${new Date().getTime()}`;
});
```

\=> 렌더링 시 항상 작동. state가 바뀔때도 실행이 됨으로&#x20;

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

\=> 위의 검색의 내용을 바꾸더라도(state 변경) 제목의 값이 변경된다.

\=> 내가 진짜 지금까지 useEffect를 잘못 사용하고 있었음...

\=> 나의 useEffect 의 사용 방법은 그냥 데이터가 새로 파생될때 항상 사용했다.

\=> 물론, return (clean up)도 제대로 하지 않았고.

\=> 그러니 말 그대로 side Effect rendering들이 다수 발생할 수 밖에 없었지...



### Clean up(return)

> return 을 통해 계속해서 실행되는 useEffect를 끝내줄 수 있다.

\=> 나는 사실 이걸 하지 않고 계속해서 \[] trriger 조건들을 부여했지..

\=> 그러니 점점 useEffect의 실행이 많아지고 이를 통해 state를 건드려 의도치 않은 rendering들로rendering 비효율을 유도하게 됨.



### 처음에 한번만 실행하기

가장 대표적으로 API를 호출해서 데이터를 얻어올 때 사용

(외부에서 영향을 받는 것)

```typescript
const [products, setProducts] = useState<Product[]>([]);

useEffect(() => {
	const fetchProducts = async () => {
		const url = 'http://localhost:3000/products';
		const response = await fetch(url);
		const data = await response.json();
		setProducts(data.products);
	};

	fetchProducts();
}, []);
```

Fetch 함수의 위치가 고민된다면, Dan Abramov의 글을 다시 보자.

\=> 이건 뭐냐면 fetchProducts라는 함수를 전역 변수로 만들어서 사용할 때만 useEffect 안에 실행하면 되지 않나? 맞긴 함 근데 해당 함수가 여러가지 다른 변수들에게 영향을 받을 경우에는 블록 안에 자기의 영역을 구축하고 있어야 코드가 꼬이지 않음. 그래서 안에 쓰는걸 Dan이 추천 하는 바임.

* [useEffect 완벽가이드 - 함수를 이펙트 안으로 옮기기](https://overreacted.io/ko/a-complete-guide-to-useeffect/#%ED%95%A8%EC%88%98%EB%A5%BC-%EC%9D%B4%ED%8E%99%ED%8A%B8-%EC%95%88%EC%9C%BC%EB%A1%9C-%EC%98%AE%EA%B8%B0%EA%B8%B0)



#### 의존성 배열을 이용해 Fetch할 때 주의사항

* [Fetching data](https://beta.reactjs.org/learn/synchronizing-with-effects#fetching-data)

\=> useEffect를 사용할때는 의존성 배열을 설정하는 것을 조심하고 신중하게 해야함.

\=> 잘못 설정하면 내가 원치 않은 타이밍에 useEffect를 실행시킬 수 가 있음

\=> 그러므로 불가피하게 의존성 배열에 데이터가 추가 되었더라도 안에 타입가드 처럼 하나의 if 문으로 조건을 추가하면 해당 함수를 실행 시키지 않는 방법을 사용할 수 있음.&#x20;



