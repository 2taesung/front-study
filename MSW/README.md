# Setting

[MSW docs](https://mswjs.io/docs/getting-started/install)



Mocking Service Worker

1. test할때, node 환경에서 fetch를 해 데이터를 이용하는 실제 서비스에 가까운 test 환경
2. 실제 개발할때도 restfull api 문서만 나왔을시 api에 의존적이지 않은 상태에서 개발 진행  가능

### Install

```bash
npm install msw --save-dev
```

개발시에만 사용



### fixtures

./fixtures/index.ts

```bash
mkdir ./fixtures
touch ./fixtures/index.ts
touch ./fixtures/products.ts
```

```typescript
import { searchResult } from './search';

export default {
  searchResult,
};
```



예시 데이터

./fixtures/products.ts

```typescript
export const searchResult = {
  total_result_count: 1,
  total_page_count: 1,
  current_page: 1,
  results: [
    {
      convert_group_title: '다나앤페타 FW',
      manager: '윤여진',
      convert_id: 2938472983,
      saved_at: '2021-08-17 11:00:00',
      count: 1,
      success_count: 1,
      fail_count: 0,
      convert_images: [
        {
          id: 1,
          image_title: '다나앤페타 FW_1',
          image_url:
            'https://s3.ap-northeast-2.amazonaws.com/queenit/convert/2938472983/다나앤페타_FW_1.jpg',
          fail_reason: null,
        },
      ],
    },
  ],
};
```



### Define mocks - Define mocks

```bash
mkdir ./src/mocks
mkdir ./src/mocks/handlers.ts
```

./src/mocks/handlers.ts

```typescript
import { http, HttpResponse } from 'msw';
import { searchResult } from '@/../fixtures/search';

export const handlers = [
  http.get('/search', () => {
    return HttpResponse.json(searchResult);
  }),
];
```



### Browser



