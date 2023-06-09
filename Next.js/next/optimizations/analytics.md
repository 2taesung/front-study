# Analytics

pages/\_app.js

```javascript
export function reportWebVitals(metric) {
  console.log(metric)
}
 
function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}
 
export default MyApp
```



reportWebVitals 함수를 통해 Web Vitals에 대한 정보를 쉽게 확인해볼 수 있음

추가로 Next.js-hydration, Next.js-route-change-to-render, Next.js-render 같은 Custom metrics도 활용 추가 가능.



