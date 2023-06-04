# 주문 상세

Record&#x20;

utility type 오랜만에 사용

```typescript
const STATUS_MESSAGES: Record<string, string> = {
  paid: '결제 완료',
};

return (
    <Container>
      <dl>
        <dt>주문 일시</dt>
        <dd>{order.orderedAt}</dd>
        <dt>주문 코드</dt>
        <dd>{order.id}</dd>
        <dt>처리 상태</dt>
        <dd>{STATUS_MESSAGES[order.status]}</dd>
      </dl>
      <Table lineItems={order.lineItems} totalPrice={order.totalPrice} />
    </Container>
  )

```
