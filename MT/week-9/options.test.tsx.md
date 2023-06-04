# Options.test.tsx - 선택 변경

### 앞에서 비슷한걸 해봐서 쉬울줄 알았음

\=> 그러나, 해당 부분은 store를 활용하고 인자들을 넣고 하는걸 이전 Option과 동일하게 해도 되는지 판단이안됨.

\=> store를 조작해서 큰 범위에서 데이터 조작을 해줘야 하는 것으로 판단..



내 코드

```javascript
it("change opttion item", () => {
    render(<Options />);



    fireEvent.change(combobox, {
      target: { value:  },
    });

    expect().toBeCalledWith({
      optionId: ,
      optionItemId: ,
    });   
});

```

\=> 뭔가 이래야할 것 같은데 사실 못했음.



정답

```javascript
  it("change opttion item", () => {
    render(<Options />);

    const [option] = options;
    const [, item] = option.items;

    const [combobox] = screen.getAllByRole("combobox");

    fireEvent.change(combobox, {
      target: { value: item.id },
    });

    expect(store.changeOptionItem).toBeCalledWith({
      optionId: option.id,
      optionItemId: item.id,
    });
  });
```





