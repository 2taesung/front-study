# Option.test.tsx - 잘못된 선택

### 2. option 선택을 잘못 했을 때,

1번을 해봐서 좀 시도가 가능하련다.

\=> 아니 ... error 처리가 코드에 없는데?

\=> 없을때의 코드가 없다구....



내 코드

```javascript
  context("when wrong selection", () => {
    it("")
  })
```



정답

```javascript
  context('when selection is changed', () => {
    it('calls “onChange” callback', () => {
      renderOption();

      const [, item] = option.items;

      fireEvent.change(screen.getByRole('combobox'), {
        target: { value: item.id },
      });

      expect(handleChange).toBeCalledWith({
        optionId: option.id,
        optionItemId: item.id,
      });
    });
  });
```





