---
description: >-
  https://nextjs.org/docs/pages/building-your-application/configuring/eslint#prettier
---

# eslint

```json
{
  //console 같은 사전 static 메서드를 인식가능
  "env": {//전역변수 
    "es6": true,
    "node": true,
    "commonjs": true,
    "es2022": true
  },

  "parserOptions": { //js 언어 옵션 설정
    "ecmaVersion": "latest",
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },

  //구문 분석을 위한거(ts구문 분석 parser)
  "parser": "@typescript-eslint/parser", 
  "extends": [
    "next/core-web-vitals",
    "prettier",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended"
  ],

  //off(0) 사용안함
  //warn(1) 경고
  //error(2) 오류
  "rules": {
    "@typescript-eslint/no-unused-vars": "error",
    "import/no-unresolved": "error", //절대경로
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

