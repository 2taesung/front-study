# next.config.js

설정보다 관습!

\=> next.js 프로젝트를 하는데 솔직히 이 파일만 잘 관리해도 된다가 중론

\=> 거기다 공식문서에 명시되어 있는 부분인데&#x20;

> However, <mark style="color:red;">none of the configs are required</mark>, and <mark style="color:red;">it's not necessary to understand</mark> what each config does. Instead, search for the features you <mark style="color:red;">need to enable or modify</mark> in this section and they will show you what to do.



주의사항 : next.config.js는 Webpack, Babel or TS로 parse 되지 않으니 최신 js 문법을 쓰면 안됨.





domain option은 Next.js에서 현재는 지양하는 패턴임



### [env](https://nextjs.org/docs/app/api-reference/next-config-js/env)

환경변수보다는 전역변수에 해당.&#x20;

bundle 파일에 포함이 무조건 된다고 함.

\=> 이 말 즉, 노출이 되는 변수다.

```javascript
module.exports = {
  env: {
    customKey: 'my-value',
  },
}
```



### [reactStrictMode](https://nextjs.org/docs/app/api-reference/next-config-js/reactStrictMode)

<mark style="background-color:orange;">reactStrictMode: false?</mark>

```javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  images: {
    domains: ['lecture-1.vercel.app'],
  },
};

module.exports = nextConfig;
```

개발시에 false로 해서 개발하는 것도 좋은 방법일 거 같긴하다.

어차피 production으로 build하면 얘는 죽어서 알아서 하나만 실행된다.



그러나 개발시에는 debuging 용도로 이걸 true로 해놓는 경우가 있는데

이러면 useEffect 구문이 의도치 않게 두번 실행되는 경우가 많다.

예를 들어, 의도치 않게 destroy 함수를 두번 실행하는 개발 상황이 됨.

```jsx
  useEffect(() => {
    return () => {
      mapRef.current?.destroy();
    };
  }, []);
```



