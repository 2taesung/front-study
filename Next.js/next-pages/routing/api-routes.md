---
description: https://nextjs.org/docs/pages/building-your-application/routing/api-routes
---

# API Routes

app router에서는 API Routes 대신에  [Server Components](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating) or [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers) 를 쓸 수 있음.



pages폴더 안에서 /api/\* 면 자동으로 page대신 api 엔드포인트로 처리.

서버 측 전용 번들러이며 클라이언트 측 번들 크기를 늘리지 않음.



API Routes 는CORS 헤더를 지정하지 않으므로  default로 **same-origin only**&#x20;

요청 핸들러를 CORS 요청 헬퍼로 래핑하여 이러한 동작을 사용자 정의할 수 있습니다.

\=> 기본적으로 ssr을 위한 것이기 때문에 나만 사용하면 됨.

\=> 그러나 외부에서 접근을 해야한다면 방법이 없는건 아님

\=> 실행 전에 cors middleware를 실행해서 한번 래핑해주는 방법이 있고&#x20;

\=> Custom config 를 활용하는 방법도 있으리라 생각.



인자인 req, res에서 다양한 메서드들 일반 api처럼 똑같이 사용 가능.

### Custom config

모든 API Route에 대해서 config를 설정할 수 있음.

사이즈 제한 등 다양한 옵션 처리를 할 수 있음.



