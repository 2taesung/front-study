# react-router-dom

```bash
npm i react-router-dom
```

```bash
mkdir src/routes
touch src/routes/routes.tsx
```

```bash
touch src/App.test.tsx
```

.src/App.test.tsx

```tsx
import { render, screen } from '@testing-library/react';
import { MemoryRouter } from 'react-router-dom';
import App from './App';

const context = describe;

describe('App', () => {
  context('when the current path is "/"', () => {
    it('renders the / page', () => {
      render(
        <MemoryRouter initialEntries={['/']}>
          <App />
        </MemoryRouter>,
      );

      screen.getByText(/Hello/);
    });
  });
});
```

./src/route/routes.tsx

```tsx
import { createBrowserRouter } from "react-router-dom";
import App from "../App";
import Layout from "./Layout";

type RouterItem = {
  path: string;
  element: JSX.Element;
};

export const RouterInfo: RouterItem[] = [
  {
    path: "/",
    element: <App />,
  },
];

export const ReactRouterObj = createBrowserRouter([
  {
    element: <Layout />,
    children: RouterInfo,
  },
]);

```

```bash
touch src/routes/Layout.tsx
```

./src/route/Layout.tsx

```tsx
import { Outlet } from "react-router-dom";
import Navbar from "../components/Navbar";

export default function Layout() {
  return (
    <>
      <Navbar />
      <Outlet />
    </>
  );
}

```

<pre class="language-bash"><code class="lang-bash"><strong>mkdir src/components
</strong><strong>touch src/components/Navbar.tsx
</strong></code></pre>

./src/components/Navbar.tsx

```bash
export default function Navbar() {
  return <>Navbar</>;
}

```

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

./src/main.jsx

```tsx
import React from 'react';
import { createRoot } from 'react-dom/client';
import { RouterProvider } from 'react-router-dom';

import { ReactRouterObj } from './routes/routes';

// Render your React component instead
const root = createRoot(document.getElementById('root') as HTMLElement);
root.render(
  <React.StrictMode>
    <RouterProvider router={ReactRouterObj} />
  </React.StrictMode>,
);
```
