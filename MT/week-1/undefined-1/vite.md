# Vite

\
vite는 vue를 타겟으로 vue 개발자가 만들었다가 다른 라이브러리들에서도 지원하게 됨.

일단 기본적인 vite의 cra 버전 명령어

```bash
yarn create vite <프로젝트명> --template react-ts
```



vite.config.ts

```typescript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
})
```



vercel을 vite로 빌딩한 파일을 올리면 / 가 아닌 다른 주소로 들어가거나 새로고침하면 버그가 발생하는 문제가 있었음



package.json과 같은 위치에 vercel.json 생성

vercel.json

```javascript
{
  "routes": [{ "src": "/[^.]+", "dest": "/", "status": 200 }]
}
```

