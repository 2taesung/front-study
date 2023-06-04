# JSX -> JS 변환 실습 코드들

#### Example #1

JSX 코드

```jsx
<p>Hello, world!</p>
```

변환된 JS 코드

```jsx
React.createElement("p", null, "Hello, world!");
```

#### Example #2

JSX 코드

```jsx
<Greeting name="world" />
```

변환된 JS 코드

```jsx
React.createElement(Greeting, { name: "world" });
```

#### Example #3

JSX 코드

```jsx
<Button type="submit">Send</Button>
```

변환된 JS 코드

```jsx
React.createElement(Button, { type: "submit" }, "Send");
```

#### Example #4

JSX 코드

```jsx
<div className="test">
	<p>Hello, world!</p>
	<Button type="submit">Send</Button>
</div>
```

변환된 JS 코드

```jsx
React.createElement(
	"div",
	{ className: "test" },
	React.createElement("p", null, "Hello, world!"),
	React.createElement(Button, { type: "submit" }, "Send")
);
```

#### Example #5

JSX 코드

```jsx
<div>
	<p>Count: {count}!</p>
	<button type="button" onClick={() => setCount(count + 1)}>Increase</button>
</div>
```

변환된 JS 코드

```jsx
React.createElement(
	"div",
	null,
	React.createElement("p", null, "Count: ", count, "!"),
	React.createElement("button", { type: "button", onClick: () => setCount(count + 1) }, "Increase")
);
```
