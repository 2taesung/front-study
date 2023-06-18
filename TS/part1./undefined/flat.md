# flat

```typescript
    flat<A, D extends number = 1>(
        this: A,
        depth?: D
    ): FlatArray<A, D>[]
```

D는 depth를 표현하고 optional이다.

왜냐하면 extends number =1 로 default 값을 줌



```typescript
type FlatArray<Arr, Depth extends number> = {
    "done": Arr,
    "recur": Arr extends ReadonlyArray<infer InnerArr>
        ? FlatArray<InnerArr, [-1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20][Depth]>
        : Arr
}[Depth extends -1 ? "done" : "recur"];
```

꼼수의 집합체

{} \[] 문법의 경우 객체 안에 있는 키를 특정하는 것.

Depth가 -1 (없냐)

없으면 "done"키로 value인 Arr로 type은 Arr 타입인걸로

Depth가 있으면 재귀로 Depth를 하나씩 낮춰줘야함..



그런데 문제는 type에서 -1 이 없음.

그래서 재귀로 하나씩 레이어를 까주는데 20까지 배열을 나열한 후 하나씩 작은 숫자를 들어가게 끔 재귀를 구현함.



infer InnerArr 안에 있는 arr의 타입을 추론하라고 시킨것.

{% embed url="https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#inferring-within-conditional-types" %}

conditional type 에 있는  infer 문법이다.



