# 섹션 2. lib.es5.d.ts 분석

[ts deep dive](https://radlohead.gitbook.io/typescript-deep-dive/type-system/lib.d.ts#native-%ED%83%80%EC%9E%85-%EC%88%98%EC%A0%95)



ts는 가독성이 안좋다.&#x20;

나만의 착각이 아니다,  다 그렇다, 그래서 라이브러리 분석을 통해 이 능력도 익히는 것



특히 generic이 만드는 커스텀 변수들이 화면을 꽉 채우는 건 어렵게 만드는 이유 중 하나

그래서 generic의 흔적을 찾아봐야함. 하나를 발견하면 다 그걸로 대입해 generic을 이해하면 됨.

{% hint style="info" %}
ts에서 콜백함수의 매개 변수는 항상 옵셔널.
{% endhint %}

forEach와예 map을 예를들어보면,

```typescript
interface Array<T> {
    forEach(callbackfn: (value: T, index: number, array: T[]) => void, thisArg?: any): void;
    map<U>(callbackfn: (value: T, index: number, array: T[]) => U, thisArg?: any): U[];
}

[1,2,3].forEach((value) => console.log(value));
const strings = [1,2,3].map((value) => value + 1);
```

forEach는 value로 들어가는 값이 number

U 역시 number로 이어지고 return 값으로 number\[]까지..



### filter

```typescript
interface Array<T> {
    filter<S extends T>(predicate: (value: T, index: number, array: readonly T[]) => value is S, thisArg?: any): S[];
    filter(predicate: (value: T, index: number, array: readonly T[]) => unknown, thisArg?: any): T[];
}

const filtered = ['1', 2, '3', 4, '5'].filter((value) => typeof value === 'string')
```

lib.es5.d.ts 에 두개가 선언이 되어있다.

둘 중에 하나 쓰면 되는거긴 함.

아무래도 내용을 보니 unknown이 없는게 나음.&#x20;

filter에서 타입추론을 잘 못해주는 경우도 있는데 한번 보자.



두번째 함수 타입에서는 T가 number or string 이 둘다 들어올 수 있음 그러므로 결과값에 정확한 추론이 안됨.

첫번째 함수 타입을 보면 number or string이될 가능성이 충분히 있다.&#x20;

그리고 이를 통해 타입추론이 가능.

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

그런데 이러면 끝이 아니라 어떻게 하면 filter 의 타입이 추론을 잘하게끔 해줄 수 있는가 고민해봐야지

한번 차근차근 대입해보면 T 는 string | number 그러면 첫번째 함수 타입도 S가 string | number가 될테니 위의 사진의 문제를 해결할수가 없다.

\=> 우리는 위의 코드에서 string\[]를 뽑아낼 수 있어야함 ....

\=> 두번째 함수타입은 T에 string | number 를 하면 끝나버린다.

\=> 그러니 string\[] 로 추론을 유도할 여지가 없음&#x20;

\=> 그러나첫번째 함수는 타입가드 역할을 하는 S 가 남아있기에 다툴 여지가 있음.

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

\=> 위와같이 함수를 따로 빼서 return 값을 구체적으로 잡아주면 우리가 원하는대로 type을 잡을 수 있음&#x20;

\=> 그러나 엄청 어거지 같은데 ....









