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



