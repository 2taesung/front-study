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
