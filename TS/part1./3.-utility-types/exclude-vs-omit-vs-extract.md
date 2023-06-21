# Exclude vs Omit / vs Extract

실습 예문

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

### Exclude

```typescript
type Exclude<T, U> = T extends U ? never : T;
```

never 가 쓰여서 원래는 never 들이 포함이 된다. 근데 안쓰여서 무시됨.

일단 여기에 never가 등장하는 이유는 알고있으셈.

```typescript
type A = Exclude<keyof Profile, 'married'>

// A = 'name | age'
```

Profile에서 'married' 속성을 제외한 타입을 구성해준다.

밑에 Omit과 다른점은 여기서는 keyof 로 배열을 잡아주어야한다는 점.

### Omit

```typescript
type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;
```

```typescript
const newZerocho: Omit<Profile, 'married'> = {
    name: 'zerocho',
    age: 29,
}
```

Pick과 Exclude가 함께 섞은 형태로&#x20;

T 와 같은 제네릭을 사용할 수 있게 됨.



### Exclude vs Omit&#x20;

exclude와 omit의 분명한 차이점에 대해 질문을 드림.&#x20;

이 둘은 용도가 전혀 아르기 때문에 같이 묶어서 생각할 여지도 없다고 생각할 수 있음

근데 나는 빼는 기능은 비슷한 것 같아 카테고리로 묶음.

Extract 역시 마찬가지&#x20;

이 둘을 분명히 구분해야할 것은&#x20;



Exclude는 유니온을 대상으로 하는 것이고

Omit은 객체를 대상으로 하는 것.

<figure><img src="../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>



Extract

```typescript
type Extract<T, U> = T extends U ? T : never;
```

```typescript
type A = Extract<keyof Profile, 'married'>

// A = 'married'
```

'married' 속성만 빼줌.
