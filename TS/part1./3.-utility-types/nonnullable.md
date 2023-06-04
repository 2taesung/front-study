# NonNullable

```typescript
type NonNullable<T> = T extends null | undefined ? never : T;
```

```typescript
type A = string | null | undefined | boolean | number;
type B = NonNullable<A>;

// B = 'string | boolean | number'
```
