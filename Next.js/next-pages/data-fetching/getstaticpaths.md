---
description: >-
  https://nextjs.org/docs/pages/building-your-application/data-fetching/get-static-paths
---

# getStaticPaths

이건 주로 Dynamic Routes이면서  getStaticProps를 사용하면 path를 정적으로 제공할 때 사용함.

이것을 통해 paths를 제공함으로 Dynamic Routes에서도 pre-rendering을 사용할 수 있다.

\=> 쉽게 말해 getStaticProps로 \[slug]는 만들어놓지 못하니 getStaticPaths가 \[slug]를 동적으로 받아 이에 맞는 것들을 미리 다 만들어주는 것.



\*참고

해당 함수도 static으로 build시에만 실행된다.

### fallback

false: 없는 페이지의 경우 404

true : 없는 페이지의 경우 에러

path가 build할 때는 없었어도 사용할때 생기면 화면에 그린다.

예를 들어, 블로그 포스팅해서 값이 생겼을때가 있겠다.



\=> 없으면 fallback이라는 flag가 살아서&#x20;

```javascript
if (router.isFallback) {
    return <div>Loading...</div>
}
```

다음과 같은 처리를 해줄 수 있다.

blocking: 없는 페이지의 경우 true와 다른 에러

\=> 없어도 좀 기다렸다가 flag 없이 보여준다.



