# 섹션 5 - Node, Express

package가 없으면 index 체크



### declare global {}

말 그대로 전역으로 선언한느 것.

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
