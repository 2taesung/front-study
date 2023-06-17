# bind

```typescript
function a(this: Window | typeof obj) {
  console.log(this.name);
}

const obj = { name: "ts" };
const b = a.bind(obj);
b();
```

```typescript
bind<T>(this: T, thisArg: ThisParameterType<T>): OmitThisParameter<T>;
```

T에 해당하는게 일단 object(typeof obj)

고로 this의 타입은 object



그럼 남은 ThisParameterType은 ?

```typescript
type ThisParameterType<T> = T extends (this: infer U, ...args: never) => any ? U : unknown;
```

T(this의 타입) 를 추론하지 못하면 unknown

추론 했으면 추론 한대로 U.





return 값인 OmitThisParameter 가보면..

```typescript
/**
 * Removes the 'this' parameter from a function type.
 */
type OmitThisParameter<T> = unknown extends ThisParameterType<T> ? T : T extends (...args: infer A) => infer R ? (...args: A) => R : T;
```

\=> 지금 조건문이 두번 중첩되어 있음.



ThisParameterType를 통해 T(this type)의 추론에 실패하면 unknown이 추론됨.

그러면 그대로 T.

그래서&#x20;

```
unknown extends ThisParameterType<T> ?
```

이 부분은 타입추론에 실패했을때? 라는 말이다. 결과적으로



그러면 그 반대는 성했을  때,

```
: T extends (...args: infer A) => infer R ? (...args: A) => R : T;
```

T는 (infer A) 매개변수 추론, => infer R 리턴값 추론 을 통해

추론에 성공했으면 이를 이용한 함수 type을 만들어라.



여기서 포인트는 보면 매개변수에 this가 없다.

왜냐하면 해당 부분의 실행은 추론이 성공한 상태인데&#x20;

성공했다는건 this가 있었다는거다.

그러므로 this 외의 매개변수를 가지고 따져보려고 해당 조건문이 있는거다.













