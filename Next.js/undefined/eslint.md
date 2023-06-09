---
description: >-
  https://nextjs.org/docs/pages/building-your-application/configuring/eslint#prettier
---

# eslint

```json
{
  "env": {
    "es6": true,
    "node": true,
    "commonjs": true,
    "es2022": true
  },

  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },

  "parser": "@typescript-eslint/parser",
  "extends": [
    "next/core-web-vitals",
    "prettier",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended"
  ],

  "rules": {
    "@typescript-eslint/no-unused-vars": "error",
    "import/no-unresolved": "error",
    "react/self-closing-comp": [
      "error",
      {
        "component": true,
        "html": true
      }
    ]
  }
}
```



아래 x 체크 필요

```typescript
{
  "plugins": ["testing-library", "jest-dom", "prettier", "@typescript-eslint"],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:testing-library/react",
    "plugin:jest-dom/recommended",
    "plugin:prettier/recommended",
    "next",
    "next/core-web-vitals"
  ],

  "rules": {
    "prettier/prettier": [
      "error",
      {
        "endOfLine": "auto"
      }
    ],
    "react/self-closing-comp": [
      "error",
      {
        "component": true,
        "html": true
      }
    ]
  }
}
```



"env", "parserOptions" 는 extends의 next에 포함되어있는듯.

