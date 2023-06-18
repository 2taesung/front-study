# 섹션 1 - jquery

@types/jquery 가면 가장 먼저 봐야할 건 package.json

그리고 types에 있는 index.d.ts



@types/jquery/index.d.ts

```typescript
/// <reference types="sizzle" />
/// <reference path="JQueryStatic.d.ts" />
/// <reference path="JQuery.d.ts" />
/// <reference path="misc.d.ts" />
/// <reference path="legacy.d.ts" />

export = jQuery;
```

\=> export = jQuery 이거 뭐지...?



이게 바로 ts에서 commonjs 라이브러리를 표시하는 방법이다.

jquery는 commonjs로 만들어졌다.

module.export = jQuery와 동일함



그럼 이제 export 하면&#x20;

import는 ?

```typescript
import $ = require('jquery');
```

이렇게 해야하고 우리가 익숙한 방식대로 하려면

```typescript
import * as $ from 'jquery';
```

로 해야함.



그런데 같은 처지인 react는&#x20;

```typescript
import React fromt 'react';
```

이렇게 하던데요 ?



tsconfig에서 <mark style="background-color:green;">esModuleInterop: true</mark> 세팅으로 인해 as 귀찮으니까 없애준것.



앞으로 확인했을 때&#x20;

export = $; 로 될 경우 commonjs

export default $; 면 esmodule (최신)



일부 이 import 문이 중요한 경우가 있다.&#x20;

내 생각에는 이 import 문이 딱히 뭐 그냥 자동으로 필요시에 추가해주는 거 아냐 ? 싶은데



예를 들어, jquery에서 import $가 안됐을 경우에는

$가 전역으로 처리되고 import $ 같은 경우에는 모듈로 이해한다.

