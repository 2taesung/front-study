# express

express

\->type

```typescript
export = e;
```

\=> commonjs module



```typescript
import * as core from 'express-serve-static-core';

declare function e(): core.Express;
```

\=> core 로 왜 이렇게 쪼개 놨느냐 ?

\=> 아마 다 이유가 있을 것 또는 히스토리라도 ...

관련 주석 존재

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

```
// This extracts the core definitions from express to prevent a circular dependency between express and serve-static
/// <reference types="node" />
```

\=>  a -> b 참조, b -> a 참조하면 순환 참조가 발생.

\=> 이것을 해결하기 위해 참조되는 부분을 따로 빼 처리하는 방식이 있음.

```typescript
export interface Express extends Application {
    request: Request;
    response: Response;
}
```



```typescript
export interface Application<
    LocalsObj extends Record<string, any> = Record<string, any>
> extends EventEmitter, IRouter, Express.Application {
    /**
     * Express instance itself is a request handler, which could be invoked without
     * third argument.
     */
    (req: Request | http.IncomingMessage, res: Response | http.ServerResponse): any;
...
```

\=> LocalsObj 에 대한게 없는데 이게 뭡니까?



\=> Record가 뭐드라? 객체 단위로 뭔가하는 건데 ...



\=> 일단 LocalsObj 는 제네릭으로&#x20;

```typescript
locals: LocalsObj & Locals;
```

locals 라는 정보에 담김

인터섹션 하는 Locals는

```typescript

export interface Locals extends Express.Locals {}
```

```typescript
declare global {
    namespace Express {
        // These open interfaces may be extended in an application-specific manner via declaration merging.
        // See for example method-override.d.ts (https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/method-override/index.d.ts)
        interface Request {}
        interface Response {}
        interface Locals {}
        interface Application {}
    }
}

```

```
   (req: Request | http.IncomingMessage, res: Response | http.ServerResponse): any;
```

\=> 여기에 있는 http는 node:http 인 @types/node의 다른 모듈이다.

\=> <mark style="background-color:green;">고로 express의 req, res는 http의 것을 확장한 것.</mark>



느낀점&#x20;

* Record 실제로 쓰이는거 처음보네 ...
* 제네릭에 왠 extends가 붙어있지 ...
*







