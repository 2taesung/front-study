# ReadOnly

```typescript
type Readonly<T> = {
    readonly [P in keyof T]: T[P];
};
```

\=> 객체의 값들을 수정 못하는 read 만 가능하게 만들어 줌

\=> 이전 기본 문법에서 만났던 readonly 를 전체에 적용하는 utility



기존의 type에서 readonly를 제거하는 방법도 존재함.

modify를 통해.

```typescript
type R<T> = {
    -readonly [key in keyof T]: T[key];
}
```

