# Theme

> [Theming](https://styled-components.com/docs/advanced#theming)

> [Create a declarations file](https://styled-components.com/docs/api#create-a-declarations-file)

디자인 시스템의 근간을 마련하는데 활용. 잘 정의하면 다크 모드 등에 대응하기 쉬움. 눈에 보이는 단편적인 정보를 넘어서, “의미”에 집중할 수 있게 됨.

\=> 이 말이 무엇이냐면 우리는 보통 색상을 정의하면 그냥 color: '#FFF'; backgoundColor: '#FFF'; 이렇게 잡곤 한다.

\=> 그러나 우리는 앞으로 이걸 우리의 나름의 의미 또는 약속을 부여해서 변수로 나타낼 수 있다.

\=> 예를들어, errColor, Primary ....&#x20;

\=> 이러한 약속들이 우리가 구축해나가야할 디자인 시스템의 근간이 된다.



일단 기본 Theme부터 정의.

```tsx
const defaultTheme = {
	colors: {
		background: '#FFF',
		text: '#000',
		primary: '#F00',
		secondary: '#00F',
	},
};

export default defaultTheme;
```

마찬가지로 App 컴포넌트에서 사용.

```tsx
import { ThemeProvider } from 'styled-components';

import { Reset } from 'styled-reset';

import defaultTheme from './styles/defaultTheme';

import GlobalStyle from './styles/GlobalStyle';

export default function App() {
	return (
		<ThemeProvider theme={defaultTheme}>
			<Reset />
			<GlobalStyle />
			<Greeting />
		</ThemeProvider>
	);
}
```

이제 “props.theme”을 쓸 수 있다.

```tsx
import { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`
	body {
		background: ${(props) => props.theme.colors.background};
		color: ${(props) => props.theme.colors.text};
	}
	
	a {
		color: ${(props) => props.theme.colors.text};
	}
	
	button,
	input,
	select,
	textarea {
		background: ${(props) => props.theme.colors.background};
		color: ${(props) => props.theme.colors.text};
	}
`;

export default GlobalStyle;
```

타입 문제를 해결하기 위해 `styled.d.ts` 파일을 작성.

```tsx
import 'styled-components';

declare module 'styled-components' {
	export interface DefaultTheme extends Theme {
		colors: {
			background: string;
			text: string;
			primary: string;
			secondary: string;
		}
	}
}
```

\=> 이렇게하면 타입 문제는 해결이 됨.



defaultTheme에서 타입을 뽑아서&#x20;

defaultTheme.ts

```typescript
const defaultTheme = {
  colors: {
    background: "linear-gradient(#F89E21, #FF6400)",
    text: "#FFFFFF",
    primary: "#F00",
    secondary: "#00F",
  },
};

export default defaultTheme;
```

Theme.ts

\=> 그러나 이 타입 문제를 더 멋지게 해결하기 위해



타입을 정의하고 defaultTheme을 맞추는 게 불편하니, 반대로 defaultTheme에서 타입을 추출하자.

```tsx
import defaultTheme from './defaultTheme';

type Theme = typeof defaultTheme;

export default Theme;
```

styled.d.ts

```typescript
import "styled-components";
import Theme from "./Theme";

declare module "styled-components" {
  export interface DefaultTheme extends Theme {}
}
```

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

\=> DefaultTheme은 테마를 적용할 수 있는 styled-components에서 제공하는 인터페이스이다.



타입 파일 변경.



다른 theme을 추가할 때 Theme 타입을 사용. 항상 defaultTheme에 먼저 항목을 추가/삭제하고, 나머지를 여기에 맞추면 된다.

```tsx
import Theme from './Theme';

const darkTheme: Theme = {
	colors: {
		background: '#000',
		text: '#FFF',
		primary: '#F00',
		secondary: '#00F',
	},
};

export default darkTheme;
```

의미를 명확히 드러냈다면, 다크 모드를 지원하는 것도 쉽다.
