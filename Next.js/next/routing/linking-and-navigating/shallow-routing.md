# Shallow Routing

data fetching 없이 URL만 바꿔주는 api

상태 손실 없음

shallow option true

```typescript
  const router = useRouter();
 
  useEffect(() => {
    // Always do navigations after the first render
    router.push('/?counter=10', undefined, { shallow: true });
  }, [])
```



url 데이터를 [`componentDidUpdate`](https://react.dev/reference/react/Component#componentdidupdate) `를 이용해 가져올 수 있음`



주의점 : Shallow routing은 current page에서의 변화만을 다룬다는 점.
