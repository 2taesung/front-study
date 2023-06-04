# Express

express 실제로 쓸줄 알고 나름의 템플릿도 존재.

그러므로 해당 부분에 큰 시간을 쓰지는 않기로 결정

강의에서 안내된 기본 설정들만 여기에 정리해놓기로.



express 기본 설정 설치

```bash
mkdir express-demo-app
cd mkdir express-demo-app
```

잊지 말고 .gitignore 파일 준비!

```bash
touch .gitignore
echo "/node_modules/" > .gitignore
```

패키지 초기화

```bash
npm init -y
```

TypeScript

```bash
npm i -D typescript
npx tsc --init
```

ESLint

```bash
npm i -D eslint
npx eslint --init
```

ts-node 설치

```bash
npm i -D ts-node
```

Express 설치

```bash
npm i express
npm i -D @types/express
```



app.ts

```typescript
import express from 'express';
import cors from 'cors';

const port = 3000;

const app = express();
app.use(cors())

app.get('/', (req, res) => {
	res.send('Hello, world!');
});

app.listen(port, () => {
	console.log(`Server running at http://localhost:${port}`);
});

app.get('/products', (req, res) => {

	const products = [
		{
			category: 'Fruits', price: '$1', stocked: true, name: 'Apple',
		},
		{
			category: 'Fruits', price: '$1', stocked: true, name: 'Dragonfruit',
		},
		{
			category: 'Fruits', price: '$2', stocked: false, name: 'Passionfruit',
		},
		{
			category: 'Vegetables', price: '$2', stocked: true, name: 'Spinach',
		},
		{
			category: 'Vegetables', price: '$4', stocked: false, name: 'Pumpkin',
		},
		{
			category: 'Vegetables', price: '$1', stocked: true, name: 'Peas',
		},
	];
	
	res.send({ products });
});
```
