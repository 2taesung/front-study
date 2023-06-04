# Reset CSS

#### Reset CSS

> [Reset Css](https://meyerweb.com/eric/tools/css/reset/)

> [styled-reset](https://github.com/zacanger/styled-reset)

패키지 설치.

```bash
npm i styled-reset
```

App 컴포넌트에서 사용.

```tsx
import { Reset } from 'styled-reset';

export default function App() {
	return (
		<>
			<Reset />
			<Greeting />
		</>
	);
}
```

