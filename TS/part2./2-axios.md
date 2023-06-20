# 섹션 2 - Axios

여기서 나오는 꿀팁

type 분석할 때,

d.ts 파일 볼때는 아래에서 위로



앞에서 언급했듯이&#x20;

맨처음 어떤 문법의 모듈인지 먼저 파악&#x20;

```typescript
export = 
```

가 있으면 commonjs require



```typescript
export default
```

가 있으면 esmodule 로import 해올 수 있는 애



axios 관련 틈새 지식

axios는 fetch를 쓰지 않고 XMLHttpRequest 를 사용함



```typescript
declare const axios: AxiosStatic;

export default axios;
```



```typescript
export interface AxiosStatic extends AxiosInstance {
  create(config?: CreateAxiosDefaults): AxiosInstance;
  Cancel: CancelStatic;
  CancelToken: CancelTokenStatic;
  Axios: typeof Axios;
  AxiosError: typeof AxiosError;
  HttpStatusCode: typeof HttpStatusCode;
  readonly VERSION: string;
  isCancel: typeof isCancel;
  all: typeof all;
  spread: typeof spread;
  isAxiosError: typeof isAxiosError;
  toFormData: typeof toFormData;
  formToJSON: typeof formToJSON;
  CanceledError: typeof CanceledError;
  AxiosHeaders: typeof AxiosHeaders;
}
```

AxiosStatic은 객체.

```typescript
export interface AxiosInstance extends Axios {
  <T = any, R = AxiosResponse<T>, D = any>(config: AxiosRequestConfig<D>): Promise<R>;
  <T = any, R = AxiosResponse<T>, D = any>(url: string, config?: AxiosRequestConfig<D>): Promise<R>;

  defaults: Omit<AxiosDefaults, 'headers'> & {
    headers: HeadersDefaults & {
      [key: string]: AxiosHeaderValue
    }
  };
}
```

현재 AxiosInstance 는 함수다.

interface라고 다 객체인건 아님.



고로 <mark style="background-color:green;">함수를 객체가 상속 받음.</mark>

이게 가능한가 ?

가능하다.



js 괴담에서 js 함수는 속성을 가질 수 있음.

```typescript
const a = () => {};
a.b = 'f';

a.create = () => {}
```

이런게 가능한셈.



고로 ts 도 가능.

또 여기서 Axios 는 class

```typescript
export class Axios {
  constructor(config?: AxiosRequestConfig);
  defaults: AxiosDefaults;
  interceptors: {
    request: AxiosInterceptorManager<InternalAxiosRequestConfig>;
    response: AxiosInterceptorManager<AxiosResponse>;
  };
  getUri(config?: AxiosRequestConfig): string;
  request<T = any, R = AxiosResponse<T>, D = any>(config: AxiosRequestConfig<D>): Promise<R>;
  get<T = any, R = AxiosResponse<T>, D = any>(url: string, config?: AxiosRequestConfig<D>): Promise<R>;
  delete<T = any, R = AxiosResponse<T>, D = any>(url: string, config?: AxiosRequestConfig<D>): Promise<R>;
  head<T = any, R = AxiosResponse<T>, D = any>(url: string, config?: AxiosRequestConfig<D>): Promise<R>;
  options<T = any, R = AxiosResponse<T>, D = any>(url: string, config?: AxiosRequestConfig<D>): Promise<R>;
  post<T = any, R = AxiosResponse<T>, D = any>(url: string, data?: D, config?: AxiosRequestConfig<D>): Promise<R>;
  put<T = any, R = AxiosResponse<T>, D = any>(url: string, data?: D, config?: AxiosRequestConfig<D>): Promise<R>;
  patch<T = any, R = AxiosResponse<T>, D = any>(url: string, data?: D, config?: AxiosRequestConfig<D>): Promise<R>;
  postForm<T = any, R = AxiosResponse<T>, D = any>(url: string, data?: D, config?: AxiosRequestConfig<D>): Promise<R>;
  putForm<T = any, R = AxiosResponse<T>, D = any>(url: string, data?: D, config?: AxiosRequestConfig<D>): Promise<R>;
  patchForm<T = any, R = AxiosResponse<T>, D = any>(url: string, data?: D, config?: AxiosRequestConfig<D>): Promise<R>;
}
```



결과적으로&#x20;

<mark style="background-color:green;">객체를 상속 받은 함수를 상속 받은 class가 됨.</mark>

ㅋㅋㅋ



그래서 axios는&#x20;

```javascript
new Axios()
axios()
axios.get()
```

이 세가지 방법이 모두 가능.





