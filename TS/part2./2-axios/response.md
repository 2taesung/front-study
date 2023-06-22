# 제네릭을 이용한 response

에러는 안뜨는데 된건가 ?

놉. 왜? 현재 any가 다수 발생하는 any-script 작성중

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

```typescript
get<T = any, R = AxiosResponse<T>, D = any>(url: string, config?: AxiosRequestConfig<D>): Promise<R>;
```

get을 다시 가져와보면

가장 먼저 들어오는 제네릭이 any로 없으면 타입을 포기해버린다. 이걸 먼저 채워줘야함.



<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

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

\=> 해결됨. 그대로 넣으면 됨. 약간 허무한 결말.

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

\=> 유기적으로 틀린 부분이 확인 되면 여지없이 빨간 줄.

\=> 뒤에 id도 차례대로 나온다.(userId를 없애면 빨간줄)



axios의 제네릭들이 default 값이 다 any여서 어디서 쓰나 싶었는데&#x20;

실제로 특별한 뭔가 기능을 하는 것은 아니였음.

단지, 사용하는데 타입 체킹 정도(위의 lint)



{% hint style="info" %}
알다시피 axios는 인자를 넣어서 사용하는 방법들이 다양하다. 실제로class로 만들거나 함수로 만들거나 이전에 배웠던 대로 상속을 하던 애들을 적절히 적용해 상용이 되고 있다.
{% endhint %}
