---
description: https://nextjs.org/docs/app/building-your-application/optimizing/images
---

# image

\<Image> 의 장점

* Type이 jpeg가 아니라 webp로 가져옴(용량 최적화)
* Size가 75kB, Time이 28ms 걸리는 파일이 => 5.4kB, 5ms 로 최적화됨.
* 자동으로 w, h 잡아줘서 Cumulative Layout Shift 를 자동으로 방지
* lazy loading, blurDataURL, placeholder 등을 옵션으로 쉽게 잡아줄 수 있음
* priority 속성을 통해 LCP를 우선 처리를 할 수 있음.

\=>이들이 또한 가능한 이유는 srcset 이라는 속성을 통해 다양한 크기로 파일들을 저장하고 있기 때문



주의점

* styled-jsx를 쓸 수 없음. <mark style="background-color:orange;">=> 이 문제는 모든걸 styled-jsx로 하려는 우리에게 문제가 될수도?</mark>
* 외부 주소의 이미지일 경우는 미리 w,h를 알 수 없어 필수로 넣어줘야함(fill로 부모 사이즈에 맞출 수 있음)
* 외부 주소 에러가 뜬다면 next.config에서 domain 세팅을 해줘야함. 그냥 단순하게 domain 추가해놓을 수 도 있긴 한데 그것보다 next에서 제안하는 remotePatterns를 하기를 추천.

\=> remotePatterns가 23년1월 출판된 책에 언급 없음 => 새로 생김

\=> 외부 주소가 들어가 있다보니 => 악의적인 침입에 데미지를 받음 그래서 그걸 막아주면서 생김





\=> 이게 가능한 이유는 next에서 파일을 static하게 가져와서 이미 들고 있기 때문.

\=> 이렇게 미리 도메인을 파악하고 있어야 최적화를 시키기 위해 미리 들고 있는게 가능.



```javascript
module.exports = {
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 's3.amazonaws.com',
        port: '',
        pathname: '/my-bucket/**',
      },
    ],
  },
};
```
