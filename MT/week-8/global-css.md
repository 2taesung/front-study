# Global CSS

#### Global Style

> [createGlobalStyle](https://styled-components.com/docs/api#createglobalstyle)

> [대체 CSS box model](https://developer.mozilla.org/ko/docs/Learn/CSS/Building\_blocks/The\_box\_model#%EB%8C%80%EC%B2%B4\_css\_box\_model)

> [box-sizing](https://developer.mozilla.org/ko/docs/Web/CSS/box-sizing)

> [The 62.5% Font Size Trick](https://www.aleksandrhovhannisyan.com/blog/62-5-percent-font-size-trick/)

> [keep-all-villain](https://twitter.com/keepallvillain)

> [word-break](https://developer.mozilla.org/ko/docs/Web/CSS/word-break)

전역 스타일 지정.

```tsx
import { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`
	html {
		box-sizing: border-box;
	}
	
	*,
	*::before,
	*::after {
		box-sizing: inherit;
	}
	
	html {
		font-size: 62.5%;
	}
	
	body {
		font-size: 1.6rem;
	}
	
	:lang(ko) {
		h1, h2, h3 {
			word-break: keep-all;
		}
	}
`;

export default GlobalStyle;
```

마찬가지로 App 컴포넌트에서 사용.

```tsx
import { Reset } from 'styled-reset';

import GlobalStyle from './styles/GlobalStyle';

export default function App() {
	return (
		<>
			<Reset />
			<GlobalStyle />
			<Greeting />
		</>
	);
}
```
