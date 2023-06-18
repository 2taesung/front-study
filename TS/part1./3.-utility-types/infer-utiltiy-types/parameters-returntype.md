# Parameters, ReturnType

### Parameters&#x20;

```typescript
type Parameters<T extends (...args: any) => any> = T extends (...args: infer P) => any ? P : never;
```

```typescript
fucntion zip(x: string, y: number): {x: string, y: number} {
    return {x, y};
}
type Params = Parameters<typeof zip>;
// Params 는 튜플 형태(인덱스로 접근 가능한)로 return 된다.
// type Params = [x: stirng, y: number]
```

이제 이 Parameters를 만들업보자

가장 먼저&#x20;

type P\<T> = ...

T는 function을 받기 때문에&#x20;

type P\<T extends (...args: any) => any> = ...

\=> 이건 함수를 받는 그냥 공식이다. => T는 함수여야된다 이거야

type P\<T extends (...args: any) => any> = T extends (...args:infer A) => any ? A: never;

\=> infer 는 extends에서만 사용 가능

\=> ts 한테 매개변수 자리를 추론하라는 것이다.

\=> 우리는 함수를 넣었으니까 함수 안에 있는 매개변수 ,  x, y 를 ts에게 직접 추론하라고 하고 사용하는 것이다.





infer 를 이용해서 return 에 args들을 뱉어놓는다.

고로

```typescript
type Params = ['string', 'number'];
```

이렇게 하드코딩으로 타입들을 넣는게 아니라

keyof object 처럼 유기적으로 가져올 수 있다.



### ReturnType

```typescript
type ReturnType<T extends (...args: any) => any> = T extends (...args: any) => infer R ? R : any;
```

infer 를 이용해 return 에 return 값을 뱉어놓는다.



<mark style="background-color:green;">=> 이들을 이용해서 어떤 함수가 있을때,</mark>

<mark style="background-color:green;">=> 자유자재로 각 함수의 매개변수 타입, 리턴 타입들을 뜯어올 수 있다.</mark>



