# 제네릭을 이용한 response

에러는 안뜨는데 된건가 ?

놉. 왜? 현재 any가 다수 발생하는 any-script 작성중

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

```typescript
get<T = any, R = AxiosResponse<T>, D = any>(url: string, config?: AxiosRequestConfig<D>): Promise<R>;
```

get을 다시 가져와보면

가장 먼저 들어오는 제네릭이 any로 없으면 타입을 포기해버린다. 이걸 먼저 채워줘야함.



<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

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

AxiosResponse 의 제네릭인 T에 정상적으로 Post가 적용되어 data에도 Post가 유기적으로 적용된 것을 확인할 수 있음.



D 제네릭의 쓰임을 살펴보면 안쓰이고 있는게 사실이다....

두번째에 있는 R(T에 의해 유기적으로 할당되는)을 넘겨서 D를 어떻게 처리하는지 궁금했는데 아직 해결되지 않음.



