# express middleware

express는 middleware가 전부다...!

### express().get()

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

위 사진을 보면 타입이 동일한 무언가가 반복돼서 나열되어 있다.

이것도 <mark style="background-color:green;">오버로딩</mark>이다.&#x20;



```typescript
get: IRouterMatcher<this, 'get'>;
```

this에 해당하는게 위 IRouterMatcher에서 T 제네릭

Method가 'get'



여기서 이 친구에 해당하는 오버로딩을 위의 수많은 (사실 오바임 5개임) 오버로딩 중 어떻게 찾아내느냐?

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

이렇게 찾아서 표시해준다!



아 ... 좋은거 배웠다 ;;

제네릭은 일단 생략하고&#x20;

인자들을 보면&#x20;

path: Route&#x20;

```typescript
Route extends string
```



...handlers

```typescript
...handlers: Array<RequestHandler<P, ResBody, ReqBody, ReqQuery, LocalsObj>>
```

... 이면 spread로 풀 수 있는 타입이라는거고 Array<> 타입으로 array 확인

<mark style="background-color:orange;">=> ... 되어있는 것은 RequestHandler\<P, ResBody, ReqBody, ReqQuery, LocalsObj> 얘를 여러개 넣을 수 있다?</mark>

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

\=> cors(), multer() 애네들 일명 미들웨어들은  RequestHandler에 해당



RequestHandler

```typescript
export interface RequestHandler<
    P = ParamsDictionary,
    ResBody = any,
    ReqBody = any,
    ReqQuery = ParsedQs,
    LocalsObj extends Record<string, any> = Record<string, any>
> {
    // tslint:disable-next-line callable-types (This is extended from and can't extend from a type alias in ts<2.2)
    (
        req: Request<P, ResBody, ReqBody, ReqQuery, LocalsObj>,
        res: Response<ResBody, LocalsObj>,
        next: NextFunction,
    ): void;
}
```







