# 상품 상세

* Null Object

{% embed url="https://refactoring.com/catalog/introduceSpecialCase.html" %}

.types.ts

```typescript
export const nullProductDetail: ProductDetail = {
  id: '',
  category: { id: '', name: '' },
  images: [],
  name: '',
  price: 0,
  options: [],
  description: '',
};
```

.stores/ProductStore.ts

```typescript
export default class ProductDetailStore {
  product: ProductDetail = nullProductDetail;

  loading = true;

  error = false;
  ...
```



* 같은 목적을 가진건 하나로 묶기

./stores/ProductStore.ts

내코드

```typescript
// TODO: 상품 상세 정보를 관리하는 Store
import { singleton } from "tsyringe";
import { Action, Store } from "usestore-ts";
import { ProductDetail, nullProductDetail } from "../types";
import { apiService } from "../services/ApiService";

@singleton()
@Store()
export default class ProductStore {
  product: ProductDetail = nullProductDetail;
  loading = true;
  error = false;

  async fetchProduct(productId: { productId: string }) {
    this.setProduct(nullProductDetail);
    this.setLoading();
    this.setError();

    const product = await apiService.fetchProduct(productId);

    this.setProduct(product);
  }

  @Action()
  setProduct(product: ProductDetail) {
    this.product = product;
  }
  @Action()
  setLoading() {
    this.loading = true;
  }
  @Action()
  setError() {
    this.error = false;
  }
}
```

아샬님 코드

```typescript
// TODO: 상품 상세 정보를 관리하는 Store
import { singleton } from "tsyringe";
import { Action, Store } from "usestore-ts";
import { ProductDetail, nullProductDetail } from "../types";
import { apiService } from "../services/ApiService";

@singleton()
@Store()
export default class ProductStore {
  product: ProductDetail = nullProductDetail;
  loading = true;
  error = false;

  async fetchProduct(productId: { productId: string }) {
    this.startLoading();

    const product = await apiService.fetchProduct(productId);

    this.setProduct(product);
  }

  @Action()
  private startLoading() {
    this.product = nullProductDetail;
    this.loading = true;
    this.error = false;
  }

  @Action()
  setProduct(product: ProductDetail) {
    this.product = product;
  }
}
```



\=> start 함수로 하나로 묶어서 표현한다.
