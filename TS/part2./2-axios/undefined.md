# 훈련의 장

```typescript
import axios, { AxiosError, AxiosResponse } from "axios";

interface A {
}

interface Post {
}

interface Created {}

(async () => {
  const ax: A = axios;
  try {
    const res1 = await ax.get<>("https://jsonplaceholder.typicode.com/posts/1");

    const res2 = ax.post<>('https://jsonplaceholder.typicode.com/posts', { title: 'a', body: 'b'})

    const res3 = ax({
      method: 'post',
      url : 'https://jsonplaceholder.typicode.com/posts',
      data : {
        title: 'a', 
        body:'b'
      }
    })
    const res4 = ax('https://jsonplaceholder.typicode.com/posts',{
      method: 'post',
      data : {
        title: 'a', body: 'b'
      }
    })
  } catch (error) {
    if (ax.isAxiosError(error)) { // 커스텀 타입 가드
      // {message: '서버 장애입니다. 다시 시도해주세요'}
      console.error((error as AxiosError<{message: string}>).response?.data.message )
    }
  }
})();


```





{% hint style="info" %}
왜 실제 axios는 복잡하게 만들어졌나?

axios의 쓰는 방법이 다양한데 이것저것 똑같이 쓸 수 있게 만들어졌기 때문에.

왜 axios에는 any가 많이 사용되었나?

일단, 하나만 required, optional 을 할 수는 없음.

그래서 다 채워진거고 any 냐 ? unknown이냐 문제는&#x20;

any보다 unknown이 그나마 나음 하지만 unknown이 없을 시기에 any가 들어가 코딩 배포가 되었을 가능성이 높음.
{% endhint %}
