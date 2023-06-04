# 로그아웃

### useCheckAccessToken.test.ts

<pre class="language-typescript"><code class="lang-typescript">import { renderHook, waitFor } from "@testing-library/react";
import useCheckAccessToken from "./useCheckAccessToken";

const setAccessToken = jest.fn();
const fetchCurrentUser = jest.fn();

jest.mock("./useAccessToken", () => () => ({
  accessToken: "",
  setAccessToken,
}));

jest.mock("../services/ApiService", () => ({
  get apiService() {
    return {
      fetchCurrentUser,
    };
  },
}));

const context = describe;

describe("useCheckAccessToken.test", () => {
  beforeEach(() => {
    jest.clearAllMocks();
  });

  context("when fetching is successful", () => {
    beforeEach(() => {
      const user = "USER";
      fetchCurrentUser.mockResolvedValue(user);
    });

    it("doesn't call 'setAccessToken'", () => {
      renderHook(() => useCheckAccessToken());

      expect(setAccessToken).not.toBeCalled();
    });
  });
<strong>
</strong>  context("when fetching is failed", () => {
    beforeEach(() => {
      fetchCurrentUser.mockRejectedValue(new Error("Bad Request"));
    });

    it("calls 'setAccess' with empty string", async () => {
      renderHook(() => useCheckAccessToken());

      await waitFor(() => {
        expect(setAccessToken).toBeCalled();
      });
    });
  });
});

</code></pre>



위의 완성된test 코드를 작성하는 중에&#x20;



아래의 스샷의 에러 때문에 고생을 하게 되는데

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

expect 안에 내가 mocking할때 정의 한 jest.fn() 이 들어가서 실행이 되지 말아야하는 상황인데 실해이 되는 문제가 발생했다.

```typescript
jest.mock("./useAccessToken", () => () => ({
  accessToken: "",
  setAccessToken,
}));

jest.mock("../services/ApiService", () => () => ({
  get apiService() {
    return {
      fetchCurrentUser,
    };
  },
}));
```

이 코드를 보시면 위의 jest.mock과 아래의 jest.mock 가 콜백 함수를 두겹으로 표현한 것을 알 수 있다.



