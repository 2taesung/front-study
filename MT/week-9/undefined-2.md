# 장바구니 보기

### backdoor.ts

.tests/backdoor.ts

```typescript
const { I } = inject();

const BACKDOOR_BASE_URL = 'https://xxxx/backdoor';

export = {
  setupDatabase() {
    I.amOnPage(`${BACKDOOR_BASE_URL}/setup-database`);
    I.see('OK');
  },
}
```



\=> 백엔드와 이 용도로 나만 쓰겠다고 약속한 api

\=> 순전히 데이터를 모두 날려버리는 용도의 api이다.

\=> 왜냐하면 모두 날려버려야 추가했을때 정확하게 추가가 된걸 테스트 하는게 가능하기 때문.



./tests/features/cart\_test.ts

```typescript
Feature("Cart");

Before(({ backdoor }) => {
  backdoor.setupDatabase();
});

Scenario("Empty cart", ({ I }) => {
  I.amOnPage("/cart");

  I.see("장바구니가 비었습니다");
});
```



### curl을 이용해 실제 데이터 넣기

```bash
curl -X POST https://xxx/cart/line-items \
  -H "Content-Type: application/json" \
  --data '
    {
      "productId": "0BV000PRO0001",
      "options": [
        {
          "id": "0BV000OPT0001",
          "itemId": "0BV000ITEM001"
        },
        {
          "id": "0BV000OPT0002",
          "itemId": "0BV000ITEM005"
        }
      ],
      "quantity": 1
    }
  '
```
