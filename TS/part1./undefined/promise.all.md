# Promise.all

실습 예제

```typescript
const p1 = Promise.resolve(1).then((a) => a + 1).then((a) => a +1).then((a) => a.toString());
const p2 = Promise.resolve(2);
const p3 = new Promise((res, rej) => {
    setTimeout(res, 1000);
});

Promise.all([p1, p2, p3]).then((result) => {
    console.log(result);
});
```



```typescript
all<T extends readonly unknown[] | []>(values: T): Promise<{ -readonly [P in keyof T]: Awaited<T[P]> }>;
```

<figure><img src="../../.gitbook/assets/image (15) (2).png" alt=""><figcaption></figcaption></figure>

\=> Promise.all의 result를 보면 위의 p1처럼 여러 then, toString 등 타입을 바꿔주는 영향들이 다수 존재하는데 이 모든걸 해결하고 정답을 뿜어낸다.

\=> Promise.all은 도대체 어떤 마법을 부린 것인가?



1. ```
   all<T extends readonly unknown[] | []>
   ```

\=> Generic 좁혀놓은것

\=> 인자는 기본적으로 배열 형태

\=> readonly로 인자인 \[p1, p2, p3] 을 수정할 수 없음



2. ```
   Promise<{ -readonly [P in keyof T]...>
   ```

\=> -readonly 는 앞의 readonly를 제거

\=> keyof 가 무엇이냐 ?

\[1, '2', undefined] 의 key 는 무엇인가 ? 0, 1, 2, length



고로&#x20;

keyof T = '0' | '1' | '2' | 'length'



3. ```
   <{ -readonly [P in keyof T]: Awaited<T[P]> }>;
   ```

위처럼 keyof 로 나온 것을 어떻게 배열로 깔끔히 처리했는가

이 Awaited는 어떤 마법을 부렸는가?



일단 T\[P]를 보면 최종적으로 T 는 배열 P는 index로 값을 return&#x20;

<figure><img src="../../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

1. 그래서 위의 사진의 Awaited 의 T는 T\[P] 인 각각의 promise인 value 들이다. (p1, p2, p3 ...)

조건들(일명 conditional type)도 많이 들어가 있는데 복잡할거다.

근데 나는 또 나름 익숙해졌다고 막 겁나고 그러지는 않음&#x20;

암튼 ts 에서도 옆에서 그래서 주석을 겁나 써놓음 ..



2. T extends null | undefined ? T

\=> conditional type으로 T가 null or undefined 이면 T 그대로 씀

\=> 근데 내가 null or undefined를 넣을 여지가 없어서 지워도 에러 없음



3. T extends object & { then(onfulfilled: infer F): any } ?

\=> 일단 T는 promise이기 때문에 object 맞음

\=> then 이라는 method가 있는 객체냐?

\=> promise 이기 때문에 안에 then 존재&#x20;

\=> 고로 then 안에 있는 ts system 안에서 onfulfilled가 작동해서 infer F

\=> F로 추론을 ts 네가 알아서 추론을 해라.

\=> 여기서 infer를 아무때나 쓸 수 있는건 아니고 extends 이고 conditional type 내부여서 사용



\=> 여기서 궁금할만한게 promise라며 그러면 여기에 Promise를 가져와서 넣어주면 되는거 아녀 ?

\=> 뭐 그렇게 해도 될듯 ? 함&#x20;

<mark style="background-color:orange;">=> 그러나 위의 코드 역시도 전혀 문제 없다 Duck Typing으로 인해.</mark>

<mark style="background-color:orange;">=> 일부만 같아도 같은걸로 쳐준다.</mark>





4. F extends ((value: infer V, ...args: any) => any) ?

여기서는 F는 함수타입이냐?



5. Awaited\<V>

\=> 재귀

\=> 재귀 맞고 V는 최종적인 return 을 다시 받은거다 쉽게 말해 위의 코드 예시에서&#x20;

\=> a+1 말함.

\=> 돌고 돌아 T에 number 등의 원시 타입으로 최종적으로 들어가게 됨.

\=> 그래서 3번 에서 false가 뜨면서 T을 타입으로 할당 됨.



```typescript
type Result = Awaited<Promise<Promise<Promise<number>>>>;
// type Result: number
```

type으로 위처럼  Promise가 중첩된 경우가 없지는 않음&#x20;

Awaited는 이걸 풀어주는 역할도 함.





\=>지금 이렇게 까봐서 알겠지만 상당히 난이도가 있음

\=> 여기서 포인트가 되는건 conditional type과 infer

\=> conditional type은 익숙해져야하고

\=> infer는 추론이지만 로직으로 인해 새로운 타입을 만들어내는 셈도 됨.





