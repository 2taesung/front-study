# 훈련의 장

ts 관련해 띵언이 나왔는데

내가 상상속으로 type을 추가할 필요 없다.

필요할 때 추가하면 돼!

```typescript
interface zQuery<> {
  text(): void;
  html(): void;
}

const $tag: zQuery<HTMLElement> = $(["p", "t"]) as zQuery<HTMLElement>;

$tag.text("123");
$tag.text(123);

$tag.text(function (index) {
  console.log(this, index);
  return true;
});

$tag.text().html(document);

```



