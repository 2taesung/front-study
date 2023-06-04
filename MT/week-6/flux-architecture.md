# Flux Architecture

[https://facebook.github.io/flux/docs/in-depth-overview/](https://facebook.github.io/flux/docs/in-depth-overview/)

기존 MVC 패턴에는 문제가 있다.&#x20;

확장 됐을시에 M, V의 양방향이 방대해지면서 복잡해지는 문제가 발생한다.

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

누가 누구한테 종속되고 누가 또 누구한테 영향을 받고...&#x20;

덩치가 커지면 커질수록 코드를 파악하기 어려워진다.



그렇기에 나온 해결책으로 Flux Architecture&#x20;

그리고 이를 대표하는게 redux.



그러나 리액트 외부에 변수가 있으면 변수의 값에 변화가 있다고 하더라도 리엑트에서의 화면에서는 변화가 표시되지 않는다. 왜냐하면 이 외부 변수의 변화는 리엑트에게 렌더링을 일으키지 않으니까.

(실제로 console로 찍어보면 데이터 변화를 확인할 수 있다.)



그래서 초기 class 컴포넌트 시절의 redux(useReducer)는 강제로 렌더링을 일으키는 forceUpdate라는 함수가 존재했다. 결국 더 나아가도 원리 자체는 forceUpdate 함수 안에 setState를 해줘서 렌더링을 하는 것.



실습을 해보면

```typescript
function useForceUpdate() {
	const [, setState] = useState({});
	return useCallback(() => setState({}), []);
}
```

```typescript
// Business Logic

const state = {
    count: 0,
}
function increase() {
    state.count += 1;
}

// UI
export default function Counter() {
    const forceUpdate = useForceUpdate();
    
    ...
    //등등이 있긴 하지만 최소화
    
    return (
        <div>{state.count}</div>
    )
}
```



이런 접근을 잘 하면, React가 UI를 담당하고 순수한 TS(JS)가 비즈니스 로직을 담당하는, 관심사의 분리를 명확히 할 수 있다.



또한, 자주 바뀌는 UI 요소에 대한 테스트 대신, 오래 유지되는(바뀌면 치명적인)비즈니스 로직에 대한 테스트 코드를 작성해 유지보수에 도움이 되는 테스트 코드를 치밀하게 작성할 수 있다.



테스트코드가 장애물이 되는 경우 중 큰 경우가 로직을 테스트하려고 하는데 관련 UI가 터지면서 생기는 애로사항이다. 이를 통해 이 문제 해결.















