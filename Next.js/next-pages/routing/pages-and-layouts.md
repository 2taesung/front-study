# Pages and Layouts

23/9/18 debuging

패캠blog 실습하다가&#x20;

pages의  post와 posts 두개의 폴더로 분리된 로직을 그냥 하나에 만들어서 작업했어.

그랬더니 create하고 post 안에 있는 \[id].js 에서 새로 생긴 페이지를 인식하는데 오래걸림.

그래서 404가 뜨고 시간이 지나서 해결이 됨.



file-system based router [concept of pages](https://nextjs.org/docs/pages/building-your-application/routing/pages-and-layouts).

When a file is added to the `pages` directory, it's automatically available as a route.



### Index routes <a href="#index-routes" id="index-routes"></a>

라우터는 자동으로 폴더 구조로 인해 index거 처리됨

* `pages/index.js` → `/`
* `pages/blog/index.js` → `/blog`



### [Nested routes](https://nextjs.org/docs/pages/building-your-application/routing/pages-and-layouts#nested-routes) <a href="#nested-routes" id="nested-routes"></a>

### [Pages with Dynamic Routes](https://nextjs.org/docs/pages/building-your-application/routing/pages-and-layouts#pages-with-dynamic-routes) <a href="#pages-with-dynamic-routes" id="pages-with-dynamic-routes"></a>

### [Layout Pattern](https://nextjs.org/docs/pages/building-your-application/routing/pages-and-layouts#layout-pattern) <a href="#layout-pattern" id="layout-pattern"></a>

footer, head, header 등 다양한 컴포넌트들을 쪼개고 재사용할 수 있음.

\_app.js 파일을 보면&#x20;

한번 App 컴포넌트에서 Component 인자를 getLayout으로 래핑하는 것을 볼 수 있음.

```javascript
import Layout from "components/Layout";

export default function App({ Component, pageProps }) {

  const getLayout = Component.getLayout || ((page) => <Layout>{page}</Layout>);

  return getLayout(<Component {...pageProps} />)

}
```



왜냐하면 react의 컴포넌트는 함수(object)이기 때문에 getLayout **이라는 api를 통해 Layout 함수를 불러올 수 있음.**

components/layout.js

```
import Navbar from './navbar'import Footer from './footer' export default function Layout({ children }) {  return (    <>      <Navbar />      <main>{children}</main>      <Footer />    </>  )}
```
