# styled-components 활용

Styled Component에 추가로 스타일을 입히는 것도 가능

```typescript
import styled from 'styled-components';

const Paragraph = styled.p`
	color: #00F;
`;

const BigParagraph = styled(Paragraph)`
	font-size: 5rem;
`;

export default function Greeting() {
	return (
		<BigParagraph>
			Hello, world!
		</BigParagraph>
	);
}
```



### 기존 컴포넌트에 스타일을 입히는 것도 가능.&#x20;

단, 기존 컴포넌트가 Class를 잡아줘야 한다는 점에 주의!

```typescript
import styled from 'styled-components';

function HelloWorld({ className }: React.HTMLAttributes<HTMLElement>) {
	return (
		<p className={className}>
			Hello, world!
		</p>
	);
}

const Greeting = styled(HelloWorld)`
	color: #00F;
`;

export default Greeting;
```



### Props 활용(typescript를 고려해야한다)

[Passed props](https://styled-components.com/docs/basics#passed-props)



```typescript
import { useBoolean } from 'usehooks-ts';

import styled, { css } from 'styled-components';

type ParagraphProps = {
	active?: boolean;
}

const Paragraph = styled.p<ParagraphProps>`
	color: ${(props) => (props.active ? '#F00' : '#888')};
	${(props) => props.active && css`
		font-weight: bold;
	`}
`;

export default function Greeting() {
	const { value: active, toggle } = useBoolean(false);
	
	return (
		<div>
			<Paragraph>
				Inactive
			</Paragraph>
			<Paragraph active>
				Active
			</Paragraph>
			<Paragraph active={active}>
				Hello, world
				{' '}
				<button type="button" onClick={toggle}>
					Toggle
				</button>
			</Paragraph>
		</div>
	);
}
```



#### 속성 추가(typescript를 고려해야한다)

> [Attaching additional props](https://styled-components.com/docs/basics#attaching-additional-props)

기본 속성을 추가할 수 있음. 불필요하게 반복되는 속성을 처리할 때 유용한데, 버튼 등을 만들 때 적극 활용함.

```tsx
import styled from 'styled-components';

const Button = styled.button.attrs({
	type: 'button',
})`
	border: 1px solid #888;
	background: transparent;
	cursor: pointer;
`;

export default Button;
```

```tsx
type ButtonProps = {
    type?: 'button' | 'submit' | 'reset';
    active?: boolean;
}

const Button = styled.button.attrs<ButtonProps>((props) => ({
    type: props.type ?? 'button',
}))<ButtonProps>`
    background: #FFF;
    color: #000;
    border: 1px solid ${(props) => (props.active ? '#F00' : '#888')};
    
    ${(props) => props.active && css`
        background: #00F;
        color: #FFF;
    `}
`
```



TS 때문에 매우 더러워진다.....

