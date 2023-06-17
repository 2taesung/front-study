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



일단 이건 두번째 인자가 있을 경우니까 infer U에서 막힘..

return 값인 OmitThisParameter 가보면..

```typescript
/**
 * Removes the 'this' parameter from a function type.
 */
type OmitThisParameter<T> = unknown extends ThisParameterType<T> ? T : T extends (...args: infer A) => infer R ? (...args: A) => R : T;
```









