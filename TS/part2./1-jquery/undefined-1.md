# 정답

```typescript
interface zQuery<T> {
  text(param?: string | number | ((this: T, index: number) => void)): this;
  html(param: Document): void;
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
