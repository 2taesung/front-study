# eslint

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

