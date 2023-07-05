# Single Source of Truth

신뢰 가능한 단일 출처

여기저기서 사용되는 말임.



<mark style="background-color:green;">하나의 상태를 나타내는 state는 한 곳에만 존재해야 한다.</mark>



제어 컴포넌트의 대표적인 예시는 input tag이다.

```javascript
<input type='text'/>
```

input tag는 사용자가 입력한 값으로 value attribute를 가지고 이는 input tag의 Dom에 value attribute 데이터를 가지고 있는 것이다.

\=> input을 통한 사용자의 입력 데이터는 DOM에 저장된다.



React docs&#x20;

제어 컴포넌트(Controlled Component)

React state를 ['신뢰 가능한 단일 출처'](single-source-of-truth.md)로 만들어 두 요소를 결합할 수 있다. 그러면 form을 렌더링하는 React 컴포넌트는 form에 발생하는 사용자 입력값을 제어한다. 이러한 방식으로 React에 의해 값이 제어되는 입력 폼 엘리먼트를 '제어 컴포넌트'라고 한다.



위에서 말했던 제어 컴포넌트처럼 상태가 두곳의 출처가 생길 수도 있다.



여기서 리액트가 이걸 제어 컴포넌트를 통해 해결해준다.





