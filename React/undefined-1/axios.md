# Axios

### interceptor



요청을 보낼때 한번 가로채는것(intercept)

왜 가로챌 필요가 있는가?



횡단 관심사로&#x20;

모든 요청에 ACCESS\_TOKEN을 포함시켜준다거나

BASE\_URL을 포함시켜준다거나 메시지를 넣어준다거나 등등을 할 수 있다.



바닐라로 class로 만들면 이러한 로직이다.

왜 class로 만들었나?

class로 만들면 statefull 하게 제작할 수 있음

(function은 stateless)

그러므로 state에 BASE\_URL도 넣고 싶고

동작으로 ACCESS\_TOKEN을 header에 포함시키고 싶고.

```javascript
class HttpClient {
  // 1. baseURL
  constructor(baseURL) {
    this.baseURL = baseURL;
  }

  // 2. 모든 fetch 전에, access_token을 추가한다.
  fetch(url, options = {}) {
    console.log("token 추가");

    return fetch(`${this.baseURL}${url}`, {
      ...options,
      headers: {
        Authorization: sessionStorage.getItem("access_token"),
        ...options.headers
      }
    });
  }
}

export const httpClient = new HttpClient(
  "https://jsonplaceholder.typicode.com/"
);
```
