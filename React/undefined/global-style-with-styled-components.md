# Global Style with styled-components

```bash
npm i styled-reset
```

[https://www.npmjs.com/package/styled-reset](https://www.npmjs.com/package/styled-reset)



App.tsx

```tsx
import { Reset } from 'styled-reset';
import GlobalStyle from './styles/GlobalStyle';

export default function App() {
  return (
    <>
      <Reset />
      <GlobalStyle />
      <p>Hello</p>
    </>
  );
}

```



GlobalStyle with styled-components

```bash
npm i styled-components
npm i -D @types/styled-components @swc/plugin-styled-components
```

Babel Plugin을 SWC에서 쓸 수 있도록 포팅한 것도 함께 설치하자(SSR 지원 등을 위한 공식 권장사항).

```bash
touch .swcrc
```

.swcrc

```typescript
{
	"jsc": {
		"experimental": {
			"plugins": [
				[
					"@swc/plugin-styled-components",
					{
						"displayName": true,
						"ssr": true
					}
				]
			]
		}
	}
}
```

<pre class="language-bash"><code class="lang-bash"><strong>mkdir src/styles
</strong><strong>touch src/styles/GlobalStyle.ts
</strong></code></pre>

./src/styles/GlobalStyle.ts

```typescript
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

