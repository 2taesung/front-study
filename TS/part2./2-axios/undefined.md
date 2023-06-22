# 정답

```typescript
import axios, { AxiosError, AxiosResponse } from "axios";

type data = {
  title: string,
  body: string
}

interface config<D=any> {
  method:'post' | 'get',
  url?: string,
  data?: D
}

interface A {
  get:<T=any, R=AxiosResponse<T>>(url: string) => Promise<R>,
  post:<T=any, R=AxiosResponse<T>, D=any>(url: string, data?: D) => Promise<R>,
  isAxiosError:<T>(error: unknown) => error is AxiosError,
  (config:config<data>):void,
  (url:string, config: config<data>): void,
}

interface Post {
  userId: number,
  id: number,
  title: string,
  body: string
}

interface Created {}
interface Data { title: string, body: string}

(async () => {
  const ax: A = axios;
  try {
    const res1 = await ax.get<Post>("https://jsonplaceholder.typicode.com/posts/1");

    const res2 = ax.post<Created, AxiosResponse<Post>, Data>('https://jsonplaceholder.typicode.com/posts', { title: 'a', body: 'b'})

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
