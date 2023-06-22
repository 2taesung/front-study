# express middleware

express는 middleware가 전부다...!

### express().get()

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

위 사진을 보면 타입이 동일한 무언가가 반복돼서 나열되어 있다.

이것도 <mark style="background-color:green;">오버로딩</mark>이다.&#x20;



```typescript
get: IRouterMatcher<this, 'get'>;
```

this에 해당하는게 위 IRouterMatcher에서 T 제네릭

Method가 'get'



여기서 이 친구에 해당하는 오버로딩을 위의 수많은 (사실 오바임 5개임) 오버로딩 중 어떻게 찾아내느냐?

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

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

<mark style="background-color:green;">=> ... 되어있는 것은 RequestHandler\<P, ResBody, ReqBody, ReqQuery, LocalsObj> 얘를 여러개 넣을 수 있다?</mark>

\=> 일반적인 인자라고 생각했을때 a, ...rest 가능

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

\=> cors(), multer() 애네들 일명 미들웨어들은  RequestHandler에 해당



\=>그 뒤에 있는 (req, res) 는 해당 위치에서 '문맥적 추론'에 따라 타입이 추론이 된다.

그런데 따로 변수로 뺄 경우 이 문맥적 추론이 작동 안할 수 있다.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

```typescript
const middleware = (req: Request, res: Response, next) => {

}
```

\=> global로 declare 하여 공유하고 있기 때문에 타입을 가져다가 쓸 수 있다.

\=> next는 없어서&#x20;

```typescript
const middleware = (req: Request, res: Response, next: express.NextFunction) => {

}
```

다음과 같이 가져와야함.



\=> 그런데 이렇게 일일히 인자에 넣을게 아니라 한번에 처리할 수 있는걸 지원한다.

```typescript
const middleware: RequestHandler = (req, res, next) => {

}
```

\=> 다음처럼 RequestHandler 를 express에서 지원하기에 가져오면 됨.

```typescript
const middleware: RequestHandler = (req, res, next) => {
  req.body.bodyType; //any
  req.params.paramType; //not any
  req.query.queryType; //not any
  res.locals.localTyp; //any
}
```

여기에 발생하는 any들도 없애주고 싶다.

관련 제네릭을 뒤집어 까보는거지 뭐.

```typescript
const middleware: RequestHandler<
    {paramType: string}, 
    {message: string}, 
    {bodyType: number}, 
    {queryType: boolean}, 
    {localType: unknown} 
  > = (req, res, next) => {
    req.body.bodyType;
    req.params.paramType;
    req.query.queryType;
    res.locals.localType;
    res.json({
      message: 'hello'
    })
  } 
```

이런식으로 제네릭을 뒤져서 값을 채워주면 된다.



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



추가 팁으로 extends http.ServerResponse, Express.Response&#x20;

이렇게 두가지를 한번에 extends 할 수 도 있다.





