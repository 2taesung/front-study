# Header.test.tsx

.Header.test.tsx

Home 버튼을 클릭 했을때 router가 적절하게 바뀌는지를 확인하고 싶음.

1. Home 버튼 클릭 후, text /Hello, world!/  찾기
2. Products 버튼 클릭 후, text 'Products' 찾기
3. Cart 버튼 클릭 후, text '장바구니' 찾기

\=> 문제는 Header component 를 렌더링하는데 버튼 클릭에 따른 위의 text들은 Header component와 다른 outlet으로 분리되어 있다.

\=> 그러므로 이걸 단순히 Header component에서 테스트를 할 수 없음.

\=> 이 부분이 test에서 해결해야하는 인터페이스에 해당하는 듯.

\=> 결국 난 스스로 해결하지는 못함.



내 시도..

```typescript
describe("Header.test", () => {
  context("render", () => {
    render(<Header />);

    it("Home Link Click", async () => {
      fireEvent.click(screen.getByText("Home"));

      await waitFor(() => {
        screen.getByText("Hello, world");
      });
    });
  });
});
```

정답 코드

```javascript
test('Header', () => {
  render(<Header />);

  screen.getByText(/Shop/);
  screen.getByRole('link', { name: 'Home' });
});
```

<mark style="background-color:orange;">=> 내가 하고자 했던 테스트는 router.test 에서 해야하는 테스트였다. 정말?</mark>

<mark style="background-color:orange;">=> Header 에 있는 클릭하면 적절하고 link의 기능까지 확인을 할 수 있어야하지 않을까?</mark>





