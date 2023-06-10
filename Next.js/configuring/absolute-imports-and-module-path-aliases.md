# Absolute Imports and Module Path Aliases

ts 트랜스파일러가 번들에 compile에 관여하기 때문에 여기서 처리를 해줘야함.

tsconfig.json

```json
{
  "compilerOptions": {
    "baseUrl": ".", //'src'
    "paths": {
      "@src/*": ["./src/*"],
      "@asset/*": ["./public/asset"]
    }
  }
}
```



.eslintrc.json

```json

  "settings": {
    "import/resolver": {
      "typescript": {}
    }
  },
```



