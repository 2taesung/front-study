# TypeScript

### interface vs type

interface만 알고 있었는데 기능이 거의 비슷한 type이라는게 있다.

[interface vs type docs](https://www.typescriptlang.org/ko/docs/handbook/2/everyday-types.html#%ED%83%80%EC%9E%85-%EB%B3%84%EC%B9%AD%EA%B3%BC-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)

일반적인 개발자는 interface를 많이 사용, 아샬님은 type을

이 둘의 핵심적인 차이는 타입은 새 프로퍼티를 추가하도록 개방될 수 없는 반면, 인터페이스의 경우는 항상 확장될 수 있다는 점.

\=> 논란의 여지가 있다는 말은 정답이 없다는 말이다. 이 두가지 도구를 모두 정확히 알고 있고 필요에따라 적절히 사용해야함.



### 배열을 Tuple로 더 깐깐하게 할수도 있음

```
let anythings: any[];

anythings = ['hp', 256];

let pair: [string, number];

pair = ['hp', 256];
```



### 매개변수를 제한하거나 할 때, 매우 유용하게 쓸 수 있

예를들어, 'food', 'toy', 'bag' 으로 매개변수를 특정해 제한하고 추론을 유도할 수 있

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

이걸 제한하는 기능만 생각할수도 있는데

function 같은데서 특히 '추론'을 많이 사용하고 효과적이다.

```
type Category = 'food' | 'toy' | 'bag';
function fetchProducts({ category }: { category: Category }) {
  console.log(`Fetch ${category}`);
}
```

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

\=> 함수를 사용할 때, 굉장히 직관적으로 변하고 효율적으로 되고 먼 훗날에 함수를 보더라도 더 이해하기 쉬워질듯 함.(이건 아직 내 추측)

\=> 아샬님 "컴파일할때 에러 잡고 보다도 이게 더 크다 "



### React에서 type 시스템으로  쓰게끔 만들어놈

예를 들어, ReactNode가 대표적

[React type code](https://github.com/facebook/react/blob/main/packages/shared/ReactTypes.js)

```typescript
export type ReactNode =
  | React$Element<any>
  | ReactPortal
  | ReactText
  | ReactFragment
  | ReactProvider<any>
  | ReactConsumer<any>;
```

ReactNode에는 얘네들이 들어갈 수 있다~~\~~~\~라고 이미 React에 있음 ;



{% hint style="info" %}
TypeScript와 별개로도 함수의 인자를 넣을 때, 좋은 예시는&#x20;

```tsx
function add(x: number, y: number = 0) { return x + y; }
>
function add(x: number, y?: number) { return x + (y || 0) }
>
type target = number | undefined;
function add(x: number, y?: target) { return x+(y || 0) }
//(굳이 타입을 사용한다면...)
```
{% endhint %}

매개변수가 오브젝트일 때 ? optional 은 많이 사용한다.

```typescript
function greeting({ name, age }: {
  name: string;
  age?: number;  
}): string {
  return age ? `${name} (${age})` : name;
```



### Intersection Type

'교집합'이라고 표현하기도 함. (cf union type은 '합집합'이라고 표현하기도함)

확실히 합집합, 교집합이라는 표현이 직관적이고 이해가 쉽다.



조금 어려운 표현으로는 '확장' 시켰다라는 표현도 적절하다.

```typescript
type Human = {
  name: string;
  age: number;
};

type Creature = {
  hp: number;
  mp: number;
};

type Person = Human & Creature;

let person: Person;

person = { name: '홍길동', age: 13, hp: 256, mp: 16 };
```

Human과 Creature 타입을 둘다 만족해야한다 (합집합)

Human에 Creature 타입을 연결시켰다 (확장)

#### Generics, Utility Types, and Tips

* [Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html)
* [Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)
* [더 좋은 타입스크립트 프로그래머로 만드는 11가지 팁](https://velog.io/@lky5697/11-tips-that-help-you-become-a-better-typescript-programmer)



{% hint style="info" %}
최근에 팀장님에게 ts의 장점에 대해서 이야기를 하다가 '어차피 꼭 ts가 아니더라도 vscode가 대략적으로 타입을 알려주던데'라고 했다. 실제로 애매하게 알고있다가 확인해보니 이러면 ts의 장점이 하나 없어지는구나 싶었다. 그런데 여기서 정확히 알게된건 코드 내부에 있는건 이렇게 알려주는데 외부 라이브러리 등을 활용할때는 ts를    쓰지않으면 어려워진다는 점.
{% endhint %}



Visual Studio Code 자동 완성 + 실시간 오류 검사

현실적으로 TS를 쓰는 가장 큰 이유.

오래된 라이브러리인 경우 d.ts 파일만 따로 패키지로 제공됨.&#x20;

최근 것들은 다 내장함.

그래서 React 설치할때 @types/\~ 를 깔았었음(package에도 여전히 존재)

* [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)
*   [DefinitelyTyped/types](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/types)

    → 전체 목록은 너무 많아서 GitHub 웹 페이지에서 다 볼 수도 없다.
*   [DefinitelyTyped/types/react](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/types/react)

    → React는 여기서 확인할 수 있다. React 18이 바로 나오고(index.d.ts), 이전 버전은 하위 폴더(디렉터리)로 따로 관리되고 있음.



실제로 React component에서 사용하는 기본  예시는&#x20;

.main.tsx

```tsx
import ReactDOM from "react-dom/client";
import App from "./App";

const element = document.getElementById('root');

if (element) {
  const root = ReactDOM.createRoot(element);

  root.render(<App name="이태성" />)
}
```

.App.tsx

```
type AppProps = {
  name: string
}

export default function App({name}: AppProps) {
  return (
    <p>Hello, {name}!</p>
  )
}
```





