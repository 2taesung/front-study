# @types/node

### declare module

@types/node 같은 경우는&#x20;

declare module 이 있다.

이것은 특정 모듈의 선언임.



우리가 이전에 봤던 @types 들은 패키지 하나가 하나의 라이브러리의 type만을 담당했다.

그러나 @types/node 같은 경우는 node 에 fs가 있고 path가 있고 등등...&#x20;

그러므로 namespace 맹키로 모듈을 구분해 가져옴.



### node 환경의 browser와의 차이

node 같은 경우는 뭔가 특별한게 아니라 js 런타임을 해주는거라고 보면 된다.

그러므로 js가 실제로 실행되는 환경인 browser랑 다르다.



msw 하면서도 이 차이점에 대해 알아본적이 있음.



여기서 또 차이가 확인되는데&#x20;

window 는 setTimeOut의 return 타입이 number(id)

node 에서는 setTimeOut의 return 타입이 NodeJS.Timeout(커스텀 객체)



### node:fs

@types/node/fs.d.ts

```typescript
declare module 'node:fs' {
    export * from 'fs';
}
```

이게 뭐냐면 'fs'로 되어 있는걸 그대로&#x20;

node:fs로 똑같이 declare 하겠다는거&#x20;



실제로 그냥 from 'fs' 로 모듈을 불러오는 것보다 'node:fs'로 불러오는 걸 권장.

이래야 node 모르는 사람도 node의 것인지를 좀더 알 수 있음&#x20;

일반인들이 만든 패키지랑 다르게



