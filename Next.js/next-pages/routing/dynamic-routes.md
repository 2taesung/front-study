---
description: https://nextjs.org/docs/pages/building-your-application/routing/dynamic-routes
---

# Dynamic Routes

쉽게 말해 \[slug].js 을 만들면 됨.

그리고 그 안에서&#x20;

```javascript
import { useRouter } from 'next/router'
 
export default function Page() {
  const router = useRouter()
  return <p>Post: {router.query.slug}</p>
}
```

이런식으로 해당 slug 변수를 가져와서 사용할 수 있음



1. 폴더 > \[slug].js
2. \[slug] > 파일
3. 폴더 > \[...slug].js
4. 겹치면 더 명시적인게 우선

### [Optional Catch-all Segments](https://nextjs.org/docs/pages/building-your-application/routing/dynamic-routes#optional-catch-all-segments) <a href="#optional-catch-all-segments" id="optional-catch-all-segments"></a>

### \[\[...slug]] <a href="#optional-catch-all-segments" id="optional-catch-all-segments"></a>

원래 slug를 표시하면 빠지면 에러임

파일마다 페이지 렌더링을 하니까.&#x20;

근데 이걸로 optional 처리를 할 수 있음 ...가 꼭 들어가야하는 점은 주의
