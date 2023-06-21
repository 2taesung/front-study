# ts-node 사용하기

{% hint style="info" %}
type 분석 팁

복잡한 generic이 나를 현혹시킨다면 전부 지우고 일단 분석해봐라.

그리고 그 다음 단계로 generic에 돌입.
{% endhint %}



axios.get

\-> type

```typescript
get<T = any, R = AxiosResponse<T>, D = any>(url: string, config?: AxiosRequestConfig<D>): Promise<R>;
```

자 여기서 보면 T, R, D 가 문제임.



```typescript
await axios.get("https://jsonplaceholder.typicode.com/posts/1");
```

그런데 우리가 보통 쓰는걸 보면 제네릭을 안쓰는 경우가 허다함.



그래서 T, R, D 는 default 값이 들어가 있는 걸 알 수 있음.



우선 T

뭔지 모르겠음.



R은 ?

AxiosResponse

```typescript
export interface AxiosResponse<T = any, D = any> {
  data: T;
  status: number;
  statusText: string;
  headers: RawAxiosResponseHeaders | AxiosResponseHeaders;
  config: InternalAxiosRequestConfig<D>;
  request?: any;
}

```

interface 객체.

generic으로 D가 하나 더 들어가네 ?

\=> 이전 단계에는 D 선언이 없었는데 여기에 있누 ...?

\=> 얼래 config도 ? optional이 아니네?



\=> 근데 T, D는 default 값이 있기 때문에 없을 수도 있는 셈.





