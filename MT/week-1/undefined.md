# 개발 환경 세팅

{% hint style="warning" %}
우리는 Node.js 를 기반으로 개발을 하는데 왜 이게 어렵냐면 계속 바뀌기 때문.&#x20;

정리하고 있는 지금도 버전이 달라지고 있음.

그러므로 앞으로 전체적인변흐름을 파악하고 변경에 대응할 수 있는 능력을 키우는게 중요
{% endhint %}

\=> 이 능력은 어떻게 키우는가?&#x20;

<mark style="background-color:orange;">=> 강의를 들으며 찾아보고 못찾으면 구체적으로 질문.</mark>

\=> 내 생각으로개발할때 개발환경을 항상 생각하면서 개발하는 습관을 갖는것?

[따라만 하면 환경 세팅 완료](https://github.com/2taesung/frontend-survival-week01/blob/2taesung/README.md)



### JavaScript(Node.js) 개발 환경 세팅(global)

1.  Node.js

    [https://nodejs.org/](https://nodejs.org/)
2. Node.js Version manager

&#x20;    우리가 NVM으로 익숙한 것.

&#x20;    속도가 빠른 fnm을 사용.

&#x20;    \- fnm (Fast Node Manager)

&#x20;      [https://github.com/Schniz/fnm](https://github.com/Schniz/fnm)

{% hint style="info" %}
내 환경은 wsl

.fnm, .node 등의 글로벌 파일들은 시스템 자체인 /home 에 존재

더불어 React는hot reloader 가 mnt/\~ 에서는 작동이 안되기 때문에 /home 이후인 곳에 폴더를 위치시킨다.
{% endhint %}

### TypeScript + React + Jest + Parcel

> mkdir \<my-app>
>
> cd \<my-app>

1. npm

> npm init

옵션들이 많이 나오는데 한번 쭉 읽어보아라.

{% hint style="info" %}
npm i -y //추가적인 옵션 질문들에 걍 다 yes 하겠다.
{% endhint %}

package.json

```
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

\=> script의 용도는

> npm run test&#x20;

하면 "echo \\"Error: no test specified\\" && exit 1" 이 쉘 스크립트가 실행된다. 딴거 쓰면 딴거 나옴.

실행 예약어들을 넣는다. 앞으로 cra를 쓰면 자동으로 생기는 dev, start 등등의 역할들.\
\
<mark style="background-color:orange;">=> 다른 기존 환경을 보니 script 폴더가 따로 있음. 강의 진행 후 파악</mark>

2. .gitignore

```
/node_modules/ //폴더라는 의미가 담김
or
node_modules/ //현재 위치
or
node_modules //아몰랑 이 이름 다.
```

[https://www.toptal.com/developers/gitignore/](https://www.toptal.com/developers/gitignore/)



3. typescript

> npm i -D typescript

{% hint style="info" %}
명령어 축약 : npm install --save -dev (= npm i -D)
{% endhint %}

<mark style="background-color:orange;">npm의 버전에대한 이야기는 없네 => 강의 듣고 내용 없으면 질문</mark>

![](<../.gitbook/assets/image (30).png>)

```
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "typescript": "^4.9.5"
  },
  "dependencies": {
    "react": "^18.2.0"
  }
}
```

\=> devDependencies는 앞에 dev가 붙어서 알듯이 개발할때 사용하는 패키지이다.

\=> 배포할때는 devDependencies를 빼고 배포가 가능한데 배포하는 크기를 조금 줄여줄 수 있다.

<mark style="background-color:orange;">=> 이 줄이는 부분의 메리트 또는 아주 작은 메리트가 있더라도 구체적으로 어느 정도의 이득인지 내가 이건 해볼 수 있을것. 해보고도 모르겠으면 질문.</mark>

\=> 또 다른 메리트는 누군가 devDependencies에 악의적으로 무슨 짓을 할수도 있는데 그걸 방지하기 위함



아무튼 이 설치로 로컬 환경의 node\_modules에 typescript 패키지가 설치되고 함께 .bin에 관련 파일들도 생성이 된다. 예를 들면, 아래의 tsc 그래서 아래의 tsc는 npx를 통해 작업이 가능한 것.

<mark style="background-color:orange;">=> .bin이 정확히 무엇인가</mark>

> npx tsc --init

tsc는 ts 컴파일러다.

npx를 사용하면 node\_modules에 패키지를 실제 설치하는게 아니라 어떤 캐시에 저장을 해 활용을 하게 됨

또한, 그래서 옛날에는 npm으로 글로벌로 tsc를 설치하곤 했는데 지금은 npx를 하면 해당 폴더 안의 node\_modules>.bin>tsc를 실행하기 때문에 굉장히 성능이 좋고 빠르다.

<mark style="background-color:orange;">=> 구체적으로 이 '캐시' 라는 거의 작동 원리나 해당 내용 지식을 알아보자</mark>



또한, 두번째에 있는 명령어로 .bin에 있는 tsc를 직접 실행시킬 수 있다.

node\_modules/.bin

```
- node_modules
ㄴ.bin
   ㄴtsc
```

> ./node\_modules/.bin/tsc&#x20;

{% hint style="info" %}
[bin파일의정체](https://simsimjae.medium.com/%ED%8C%A8%ED%82%A4%EC%A7%80-%EC%95%88%EC%97%90%EB%8A%94-bin%EC%9D%B4%EB%9D%BC%EA%B3%A0%ED%95%98%EB%8A%94-%EC%88%A8%EA%B9%80-%ED%8F%B4%EB%8D%94%EA%B0%80-%EC%A1%B4%EC%9E%AC%ED%95%9C%EB%8B%A4-%EC%9D%B4-%ED%8F%B4%EB%8D%94%EB%8A%94-%EB%AD%90%EB%95%8C%EB%A7%A4-%EC%9E%88%EB%8A%94%EA%B1%B4%EC%A7%80-%EA%B6%81%EA%B8%88%ED%95%B4%EC%84%9C-%EC%B0%BE%EC%95%84%EB%B3%B4%EC%95%98%EB%8B%A4-8257ddaa1a7e)
{% endhint %}

```
Created a new tsconfig.json with:
                                                                                                                    TS
  target: es2016
  module: commonjs
  strict: true
  esModuleInterop: true
  skipLibCheck: true
  forceConsistentCasingInFileNames: true

You can learn more at https://aka.ms/tsconfig
```

다음 설정을 가진&#x20;

tsconfig.json 생성

기존에 파악하고 있던 tsconfig 속성 외로 추가 되는 정보

> jsx: 'preserve'
>
> or jsx: 'react'
>
> or jsx: 'react-jsx' (아샬의 픽)

아래는 jsx 속성관련 공식문서 정보&#x20;

[https://www.typescriptlang.org/tsconfig#jsx](https://www.typescriptlang.org/tsconfig#jsx)

\+ 추가

```javascript
  parserOptions: {
     // ...(전략)...
     tsconfigRootDir: __dirname,  	
  }
```

이 옵션을 추가해줘야 tsconfig의 RootDirectory가 바로 현재 실행하는 절대경로로 세팅됨

3. ESLint

> npm i -D eslint

linting 정적 분석기

패키지 설치 했으니 npx 할수 있음(복습)

> npx eslint --init

관련 설정들을 해주어야한다.

```
What type of modules does your project use?
>JavaScript modules (import/export)
```

\=> 어차피 Parcel로 번들링 해서 쓸거라서 모듈을 직접  활용하는 require/exports 가 아니여도 괜찮다.

{% hint style="info" %}
Vite 를 쓰면 또 es module?? 을 적극적으로 쓰기도 한다.
{% endhint %}

```
Which style guide do you want to follow?
>xo-typescript(아샬의픽)
```

{% hint style="info" %}
airbnb가 최근 빠짐 ..
{% endhint %}

```
eslint-plugin-react@latest eslint-config-xo@ .......
Would you like to install them now?
>Yes
```

여러가지 추가적인 설정 및 설치를 했기에 그거를 호환해준다는 말

.eslintrc.js

```javascript
module.exports = {
	env: {
		browser: true,
		es2021: true,
	},
	extends: [
		'plugin:react/recommended',
		'plugin:react/jsx-runtime', //reat 일일히 import 안해도 lint 안때림
		'xo',
	],
	overrides: [
		{
			extends: [
				'xo-typescript',
			],
			files: [
				'*.ts',
				'*.tsx',
			],
		},
	],
	parserOptions: {
		ecmaVersion: 'latest',
		sourceType: 'module',
	},
	plugins: [
		'react',
	],
	rules: {
	},
};
```

\=> 원래는 몇가지 rule들을 추가하기도 함.

아직 설치   전에도 jest 추가 가

```javascript
env: {
	browser: true,
	es2021: true,
	jest: true,
},
```

잊지말고&#x20;

> touch .eslintignore

eslint 실행할때 여기는 뺄거야

```
/node_modules/
/dist/
/.parcel-cache/
```

기본적으로 이렇게 삼종세트(gitignore랑 똑같이 해도 됨)



4. react, react-dom

> npm i react react-dom

> npm i -D @types/react @types/react-dom

{% hint style="info" %}
최근에는 이렇게 @types를 안해도 내장을 하곤 함.

그러나 옛날것들은 이렇게 같이 설치해줘야함.
{% endhint %}



5. 테스트 도구 설치

> npm i -D jest @types/jest @swc/core @swc/jest\
> jest-environment-jsdom\
> @testing-library/react @testing-library/jest-dom

기본적인 jest가 아니라 swc <mark style="background-color:orange;">=> 잘모르는   내용. 관련해서는 공부해보자</mark>

이 또한 내용이 계속 바뀔 수 있다. 당황하지 말고 맥락을 이해하고 있어서 문서를 봐서 맞게 변경해줘야함

예를들어, 맥락 "Jest와 swc를 이용" <mark style="background-color:orange;">=> 좀더 구체적으로 이 맥락이라는 거에 대한 탐구를</mark>



jest가 기본적으로 swc, ts를 잡아주지 않고 있다.

그래서 jest config를 통해서 이러한 설정들을 적용해줘야함.

> touch jest.config.js

```javascript
module.exports = {
  testEnvironment: 'jsdom',
  setupFilesAfterEnv: [
    '@testing-library/jest-dom/extend-expect', //는 사실 설치를 위에서 하긴 함
    './jest.setup', //이건 안쓴다 지워
  ],
  transform: {
    '^.+\\.(t|j)sx?$': ['@swc/jest', {
      jsc: {
        parser: {
          syntax: 'typescript',
          jsx: true,
          decorators: true,
        },
        transform: {
          react: {
            runtime: 'automatic',
          },
        },
      },
    }],
  },
  testPathIgnorePatterns: [
    '<rootDir>/node_modules/',
    '<rootDir>/dist/',
  ],
};
```

[https://github.com/ahastudio/CodingLife/blob/main/20220726/react/jest.config.js](https://github.com/ahastudio/CodingLife/blob/main/20220726/react/jest.config.js)



6. Parcel 설치

> npm i -D parcel

package.json&#x20;

```json
{
  "name": "react",
  "version": "1.0.0",
  "description": "",
  "source": "./index.html", //원래는 "main": "index.js"로 되어있다.
  "scripts": {
    "start": "parcel --port 8080",
    "build": "parcel build", //dist 파일 생성
    "check": "tsc --noEmit", // tsc 컴파일을 진행하지 않고 체크만
    "lint": "eslint --fix --ext .js,.jsx,.ts,.tsx .", // 형식들 적용
    "test": "jest",
    "coverage": "jest --coverage --coverage-reporters html",
    "watch:test": "jest --watchAll"
  },
  ...
}
```



7. html, js 기본환경셋팅

> touch index.html

index.html

````
```html
<body>
  <p>Hello, world!</p>
  <script type="module" src="./src/main.tsx"></script>
</body>
```
````

{% hint style="info" %}
원래는 esmodule이 변환을 해주는데 parcel이 번들링을 해준다.
{% endhint %}

> mkdir src
>
> touch src/main.tsx



8. 내친김에 React 기본 셋팅까

여기서 중요한게 간단한 개발 기본 습관? 을 엿볼수 있었는데

1\) 적절한 환경셋팅으로 개발 환경 및 에러 신뢰도 있게 관리(ts, eslint 등)

2\) 에러 발생하면 들어가(ctrl+click) 코드를 까본다.

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

```typescript
export function createRoot(container: Element | DocumentFragment, options?: RootOptions): Root;
```

3\) 원인을 발견한다.&#x20;

* ts에서 ReactDOM.createRoot()함수에는  container라는 인자가 있어야하고  option은 선택적
* 이 인자는 container 인자의 type까지 들어가서 체크 element or DocumentFragment

4\) 코드에 적용함 에러 사라짐(반복)

아무튼 위의 과정을 거치면 됨 아래는 리액트 최초 적용

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

element null인 경우를 방어.

```tsx
import ReactDOM from "react-dom/client";

const element = document.getElementById('root');

if (element) {
  const root = ReactDOM.createRoot(element);

  root.render(<p>Hi</p>);
}
```



```tsx
import ReactDOM from "react-dom/client";

function App() {
  return (
    <p>Hello, world!</p>
  )
}

const element = document.getElementById('root');

if (element) {
  const root = ReactDOM.createRoot(element);

  root.render(<App/>);
}
```



5\)  끝.
