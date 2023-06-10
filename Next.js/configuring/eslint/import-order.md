---
description: https://velog.io/@eenaree/eslint-import-order
---

# import/order

{% embed url="https://yarnpkg.com/package/eslint-plugin-import" %}

```bash
yarn add -D eslint-plugin-import
```

기본적으로 존재하는 sort-import 내장 모듈이 있긴 한데 제한적이다.

해당 패키지를 통해 import 성격들을 트래킹할 수 있음.&#x20;



### 사용법 설명

{% embed url="https://github.com/import-js/eslint-plugin-import/blob/main/docs/rules/order.md" %}

```json
"import/order": [
      "error",
      {
        "groups": [
          "index",
          "sibling",
          "parent",
          "internal",
          "external",
          "builtin",
          "object",
          "type"
        ],
        "alphabetize": {
          "order": "asc" /* sort in ascending order. Options: ['ignore', 'asc', 'desc'] */,
          "caseInsensitive": true /* ignore case. Options: [true, false] */
        },
        "newlines-between": "always"
      }
    ]
```





