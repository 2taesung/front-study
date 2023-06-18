# Partial vs Pick / vs Required

실습예문.

```typescript
interface Profile {
    name: string,
    age: number,
    married: boolean,
}

const zerocho: Profile = {
    name: 'zerocho',
    age: 29,
    married: false,
};

const newZerocho : ... = {
    ...
}
```

### Partial

```typescript
type Partial<T> = {
    [P in keyof T]?: T[P];
};
```

```typescript
const newZerocho: Partial<Profile> = {
    name: 'zerocho',
}
```

T에 모든 속성들을 ? 옵셔널로 바꿔준다.

\=> 근데 사실 이러면 너무 치트키 때려버리는 느낌.

### Pick

```typescript
type Pick<T, K extends keyof T> = {
    [P in K]: T[P];
};
```

```typescript
const newZerocho: Omit<Profile, 'married'> = {
    name: 'zerocho',
    age: 29,
}
```

K 라는 키 값을 선택해서 옵셔널(?)로 바꿔줄 수 있다.

\=> 치트키 Partial 보다 사용을 권장.

\=> 왜 extends keyof 여야하는가?

\=> Pick의 두번째 제네릭으로 들어가는 값은 Profile과 전혀 생뚱 맞은게 들어갈 수 없다.

\=> 그러므로 T의 키들 중에 K를 생성하는 것.



### Required

```typescript
type Required<T> = {
    [P in keyof T]-?: T[P];
};
```

```typescript
const newZerocho: Required<Profile> = {
    name: 'zerocho',
    age: 29,
    married: false,
}
```

\=> 모든 속성값이 필수로 들어가야한다. (기존 ? 도)

\=> -? 가 modify 라고 해서 옵셔널을 빼주는 문법
