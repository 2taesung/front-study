# Record

```typescript
type Record<K extends keyof any, T> = {
    [P in K]: T;
};
```

key 값에는 string | numaber | symbol 만 가능.

이게 뜻하는게 extends keyof any



```typescript
interface PageInfo {
    title: string;
}

type Page = 'home' | 'about' | 'contact';

const x: Record<Page, PageInfo> = {
    about: { title: 'about' },
    contact: { title: 'contact' },
    home: { subTitile: 'home' },
    // Error: '{ subTitile: string; }' is not assignable
    main: { title: 'home' },
    // Error: main is not assignable to type 'Page'.
};    
```

객체 단위에서 type을 적용하고 싶을 때 사용.

각각의 home, about, contract 속성에 PageInfo 라는 interface type을 적용시킴.
