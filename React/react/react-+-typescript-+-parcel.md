# React + TypeScript + Parcel



### 처음부터 따라하기

#### npm 프로젝트 생성

```shell
npm init -y  
```

#### 잊지말고 .gitignore

```shell
touch .gitignore
```

```.gitignore
/node_modules/
/dist/
/.parcel-cache/
```

#### TypeScript 세팅

```shell
npm i -D typescript  
npx tsc --init  
```

tsconfig.json 에서 수정

```json
{
  "compilerOptions": {
    // ...(전략)...
    "jsx": "react-jsx",
    // ...(후략)...
  },
}
```

#### ESLint 세팅

```shell
npm i -D eslint  
npx eslint --init
```

#### XO 관련 의존성 제거하고, 에어비앤비 관련 의존성 설치.

```shell
npm uninstall eslint-config-xo \
    eslint-config-xo-typescript

npm i -D eslint-config-airbnb \
    eslint-plugin-import \
    eslint-plugin-react \
    eslint-plugin-react-hooks \
    eslint-plugin-jsx-a11y
```

.eslintrc.js 에서 섬세하게 수정

```js
module.exports = {
    env: {
        browser: true,
        es2021: true,
        jest: true,
    },
    extends: [
        'airbnb',
        'plugin:@typescript-eslint/recommended',
        'plugin:react/recommended',
        'plugin:react/jsx-runtime',
    ],
    parser: '@typescript-eslint/parser',
    parserOptions: {
        ecmaVersion: 'latest',
        sourceType: 'module',
    },
    plugins: [
        'react',
        '@typescript-eslint',
    ],
    settings: {
        'import/resolver': {
        node: {
                extensions: ['.js', '.jsx', '.ts', '.tsx'],
            },
        },
    },
    rules: {
        indent: ['error', 2],
        'no-trailing-spaces': 'error',
        curly: 'error',
        'brace-style': 'error',
        'no-multi-spaces': 'error',
        'space-infix-ops': 'error',
        'space-unary-ops': 'error',
        'no-whitespace-before-property': 'error',
        'func-call-spacing': 'error',
        'space-before-blocks': 'error',
        'keyword-spacing': ['error', { before: true, after: true }],
        'comma-spacing': ['error', { before: false, after: true }],
        'comma-style': ['error', 'last'],
        'comma-dangle': ['error', 'always-multiline'],
        'space-in-parens': ['error', 'never'],
        'block-spacing': 'error',
        'array-bracket-spacing': ['error', 'never'],
        'object-curly-spacing': ['error', 'always'],
        'key-spacing': ['error', { mode: 'strict' }],
        'arrow-spacing': ['error', { before: true, after: true }],
        'import/no-extraneous-dependencies': ['error', {
            devDependencies: [
            '**/*.test.js',
            '**/*.test.jsx',
            '**/*.test.ts',
            '**/*.test.tsx',
        ],
        }],
        'import/extensions': ['error', 'ignorePackages', {
            js: 'never',
            jsx: 'never',
            ts: 'never',
            tsx: 'never',
        }],
        'react/jsx-filename-extension': [2, {
            extensions: ['.js', '.jsx', '.ts', '.tsx'],
        }],
        'jsx-a11y/label-has-associated-control': ['error', { assert: 'either' }],
    },
};
```

그냥 통짜로 바꿔버리자, 하나하나는 gitbook에서

#### 잊지말고 .eslintignore

```shell
touch .eslintignore
```

```.eslintignore
/node_modules/
/dist/
/.parcel-cache/
```

#### React-dom세팅

```shell
npm i react react-dom  
npm i -D @types/react @types/react-dom
```

#### VS Code 설정 파일 생성

.vscode 디렉터리 및 settings.json 파일 생성.

```shell
mkdir .vscode
touch .vscode/settings.json
```

.vscode/settings.json 파일은 다음과 같이 작성한다.

```json
{
    "editor.rulers": [
        80
    ],
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    "trailing-spaces.trimOnSave": true
}
```

#### Jest 세팅

Jest 및 SWC 지원 패키지 설치.

```shell
npm i -D jest @types/jest @swc/core @swc/jest
touch jest.config.js
```

jest.config.js

```js
module.exports = {
  // testEnvironment: 'jsdom',
  // setupFilesAfterEnv: [
  //   '<rootDir>/src/setupTests.ts',
  // ],
  transform: {
    '^.+\\.(t|j)sx?$': ['@swc/jest', {
      jsc: {
        parser: {
          syntax: 'typescript',
          // jsx: true,
          // decorators: true,
        },
        transform: {
          // react: {
          //   runtime: 'automatic',
          // },
          // legacyDecorator: true,
          // decoratorMetadata: true,
        },
      },
    }],
  },
};
```

#### React Testing Library 세팅

```shell
npm i -D @testing-library/react jest-environment-jsdom
```

jest.config.js 파일에서 관련 항목의 주석을 풀어준다.

```json
module.exports = {
  testEnvironment: 'jsdom',
  // setupFilesAfterEnv: [
  //   '<rootDir>/src/setupTests.ts',
  // ],
  transform: {
    '^.+\\.(t|j)sx?$': ['@swc/jest', {
      jsc: {
        parser: {
          syntax: 'typescript',
          jsx: true,
          // decorators: true,
        },
        transform: {
          react: {
            runtime: 'automatic',
          },
          // legacyDecorator: true,
          // decoratorMetadata: true,
        },
      },
    }],
  },
};
```

#### Parcel 세팅

```shell
npm i -D parcel
touch .parcelrc.json
```

```json
{
  "extends": ["@parcel/config-default"],
  "reporters":  ["...", "parcel-reporter-static-files-copy"]
}
```

package.json

```json
  "scripts": {
    "start": "parcel --port 8080",
    "build": "parcel build", 
    "check": "tsc --noEmit", 
    "lint": "eslint --fix --ext .js,.jsx,.ts,.tsx .",
    "test": "jest",
    "coverage": "jest --coverage --coverage-reporters html",
    "watch:test": "jest --watchAll"
  },
```

#### vscode 세팅

```shell
mkdir .vscode  
touch .vscode/settings.json  
```

```json
{
    "editor.rulers": [
        80
    ],
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    "trailing-spaces.trimOnSave": true
}
```

#### html, js 기본환경세팅

`package.json`

```json
{
  // ...(전략)...
  "source": "index.html",
  // ...(후략)...
}
```

```shell
touch index.html
```

`index.html` 파일 작성.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>React Demo App</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="./src/main.tsx"></script>
  </body>
</html>
```

```shell
mkdir src
touch src/main.tsx
```

`src/main.tsx`

```js
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";

import App from './App';

const root = createRoot(document.getElementById("root") as HTMLElement);
root.render(<App />);
```

`src/App.tsx`

```js
export default function App() {
  return (
    <p>Hello, world!</p>
  );
}
```

테스트 파일

```shell
touch src/App.test.tsx
```

<pre class="language-tsx"><code class="lang-tsx"><strong>import { render, screen } from '@testing-library/react';
</strong>
import App from './App';

test('App', () => {
  render(&#x3C;App />);

  screen.getByText(/Hello, world/);
});
</code></pre>
