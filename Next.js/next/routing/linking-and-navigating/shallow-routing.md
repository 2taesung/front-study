# Shallow Routing

data fetching 없이 URL 바꿔주는 api

```typescript
  const router = useRouter();
 
  useEffect(() => {
    // Always do navigations after the first render
    router.push('/?counter=10', undefined, { shallow: true });
  }, [])
```
