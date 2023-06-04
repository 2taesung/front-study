# ConstructorParameters, InstanceType

### ConstructorParameters

```typescript
type ConstructorParameters<T extends abstract new (...args: any) => any> = T extends abstract new (...args: infer P) => any ? P : never;
```

<pre class="language-typescript"><code class="lang-typescript">type T10 = ConstructorParameters&#x3C;ErrorConstructor>; // [(string | undefined)?]
type T1 = ConstructorParameters&#x3C;FunctionConstructor>; // string[]
type T2 = ConstructorParameters&#x3C;RegExpConstructor>; // [string, (string | undefined)?]

interface I1 {
<strong>    new(args: string): Function;
</strong>}
type T12 = ConstructorParameters&#x3C;I1>; // [string]

function f1(a: T12) {
    a[0]
    a[1] // Error: Tuple type '[args: string]' of length '1' has no element at index '1'.
}
</code></pre>

생성자 함수 타입의 모든 매개변수 타입을 추출한다. 모든 매개변수 타입을 가지는 튜플 타입(T가 함수가 아닌 경우 never)을 생성한다.



### InstanceType

```typescript
type InstanceType<T extends abstract new (...args: any) => any> = T extends abstract new (...args: any) => infer R ? R : any;
```

