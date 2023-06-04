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
```

```typescript
import products from './products';

export default {
  products,
};
```



예시 데이터

./fixtures/products.ts

```typescript
import { ProductType } from '../src/types';

const products: ProductType[] = [
  {
    id: 1,
    name: 'Warmwhite Cup',
    thumbnail:
      'https://contents.sixshop.com/thumbnails/uploadedFiles/183003/product/image_1634831270597_1000.jpg',
    price: 25000,
    category: '악세사리',
    quantity: 10,
  },
  {
    id: 2,
    name: 'Coin Walnut Table',
    thumbnail:
      'https://contents.sixshop.com/thumbnails/uploadedFiles/183003/product/image_1634415880172_1000.png',
    price: 120000,
    category: '악세사리',
    quantity: 10,
  },
];

export default products;
```



### Define mocks - Define mocks

```bash
mkdir ./src/mocks
```

./src/mocks/handlers.ts

```typescript
import { rest } from 'msw';
import { ProductType } from '../types';
import fixtures from '../../fixtures';

export const handlers = [
  rest.get('/products/:id', (req, res, ctx) => {
    const { id } = req.params;
    const filtered = fixtures.products.filter(
      (product: ProductType) => product.id === Number(id),
    );
    return res(ctx.status(200), ctx.json({ data: { product: filtered[0] } }));
  }),
];
```



### Browser



