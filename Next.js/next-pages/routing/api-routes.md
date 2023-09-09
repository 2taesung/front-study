---
description: https://nextjs.org/docs/pages/building-your-application/routing/api-routes
---

# API Routes

app router에서는 API Routes 대신에  [Server Components](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating) or [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers) 를 쓸 수 있음.



pages폴더 안에서 /api/\* 면 자동으로 page대신 api 엔드포인트로 처리.

서버 측 전용 번들러이며 클라이언트 측 번들 크기를 늘리지 않음.



API Routes 는CORS 헤더를 지정하지 않으므로  default로 **same-origin only**&#x20;

요청 핸들러를 CORS 요청 헬퍼로 래핑하여 이러한 동작을 사용자 정의할 수 있습니다.



