# Absolute Imports and Module Path Aliases

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
```



