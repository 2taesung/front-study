# express

```typescript
export = e;
```

\=> commonjs module



```typescript
declare function e(): core.Express;
```



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



\=> Record가 뭐드라?

\=>&#x20;



