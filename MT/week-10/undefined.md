# 로그인

### login test 코드에서쓰지 않는 waitFor 를 남겨놓은 이유

routes.test.tsx

```typescript
context('when the current path is "/login', () => {
    it("renders the login page", async () => {
      renderRouter("/login");

      screen.getByRole("heading", { name: "로그인" });

      await waitFor(() => {
        screen.getByText(/Category #1/);
      });
    });
  });
```

<mark style="background-color:green;">헤더에서 카테고리를 요청하는데 테스트가 안기다리고 넘어간다.</mark>&#x20;

\=> header는 모든 페이지를 렌더링 할때 같이 렌더링이 된다.

\=> router outlet과 분리되어 상단에 무조건 렌더링 하기 때문에&#x20;

\=> 그런데 header에는 비동기 함수가 포함된 hooks 기능이 있다.

\=> 그러므로 이 비동기 코드 때문에 우리가 이 비동기를 테스트 하려는 건 아니지만&#x20;

\=> 에러를 발생시킨다.

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

\=> 다시한번 반성하지만 에러를 철저하게 분석하고 구글링, 질문을 하자.



### default props property&#x20;

```typescript
type ButtonProps = {
  type?: 'button' | 'submit' | 'reset';
}
```

```typescript
const Button = styled.button.attrs<ButtonProps>((props) => ({
  type: props.type ?? 'button',
}))`
  border: .1rem solid ${(props) => props.theme.colors.primary};
  background: transparent;
  color: ${(props) => props.theme.colors.primary};
  cursor: pointer;

  :disabled {
    filter: grayscale(80%);
    cursor: not-allowed;
  }
`;
```

props의 property 중 하나인 type이 아무것도 없을 경우 button으로 자동 설정된다.

UI 라이브러리들에서 많이 사용하는 기능들이라 생각됨.



그런데 이 기능은 eslint에 문제를 발생시켜 해당 설정을 추가해줘야함

```typescript
'react/require-default-props': [2, { functions: 'defaultArguments' }],
```

\=> 그러나 추가 안했음에도 아직 문제 발생 없음



이 덕분에&#x20;

.loginForm

```typescript
        <TextBox
          label="E-mail"
          placeholder="tester@example.com"
          value={email}
          onChange={handleChangeEmail}
        />
        <TextBox
          label="Password"
          type="password"
          value={password}
          onChange={handleChangePassword}
        />
```

필수 property인 type을 생략 가능.

근데 일관성이 없어 보이기 때문에 적절한 예시는 아닌 것 같다.



<mark style="background-color:orange;">:disable 일때는 추후 두고 보기</mark>



### 이중부정(!!)

null 이나 undefined를 false로 변환할 때 사용.



### api 에 accessToken 넣어주기



```typescript
private accessToken = '';

setAccessToken(accessToken: string) {
  if (accessToken === this.accessToken) {
    return;
  }

  const authorization = accessToken ? `Bearer ${accessToken}` : undefined;

  this.instance = axios.create({
    baseURL: API_BASE_URL,
    headers: { Authorization: authorization },
  });

  this.accessToken = accessToken;
}
```

\=> 기존과 동일하면 그냥 return

\=>있으면 instanse의 headers에 꽂아서 인증

\=> undefined이면 자동으로 안가진다.



useAccessToken에서 accessToken 적용

```typescript
export default function useAccessToken() {
  const [accessToken, setAccessToken] = useLocalStorage('accessToken', '');

  useEffect(() => {
    apiService.setAccessToken(accessToken);
  }, [accessToken]);

  return { accessToken, setAccessToken };
}
```

