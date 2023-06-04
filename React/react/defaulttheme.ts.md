# defaultTheme.ts

./src/App.tsx

```tsx
import { ThemeProvider } from 'styled-components';
import { Reset } from 'styled-reset';
import GlobalStyle from './styles/GlobalStyle';
import defaultTheme from './styles/defaultTheme';

export default function App() {
  return (
    <ThemeProvider theme={defaultTheme}>
      <Reset />
      <GlobalStyle />
      <p>Hello</p>
    </ThemeProvider>
  );
}
```



./src/styles/defaultTheme.ts

```typescript
const defaultTheme = {
  colors: {
    background: '#FFFFFF',
    text: '#000000',
    primary: '#F00',
    secondary: '#00F',
  },
};

export default defaultTheme;
```



./src/styles/styled.d.ts

```typescript
import 'styled-components';
import Theme from './Theme';

declare module 'styled-components' {
  export interface DefaultTheme extends Theme {}
}
```

