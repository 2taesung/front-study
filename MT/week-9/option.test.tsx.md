# Option.test.tsx - 선택 변경

### 1. option 선택이 바뀌었을 때,

handleChange을 이용해 인자를 커스텀해서 넣고 결과를 살펴봄.

\=> 인자가 없는 함수였는데 내가 추가를 했는데 되나?

\=> 인자로 넣는 custom object의 키들이 optionId, optionItemId 같은 screen으로 볼 수 있는게 아님.

\=> 뭘로 해야할까 .... 뭘로 해야할까 ...

\=> 화면에 드러나지 않는 데이터들을 어떻게 테스트하지...?



내 코드

```javascript
  it("change option", () => {
    const custom = {
      optionId: "1",
      optionItemId: "2",
    };
    renderOption(custom);

    // fireEvent.click(screen.)
  });
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





