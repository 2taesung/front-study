# next.config.js

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



