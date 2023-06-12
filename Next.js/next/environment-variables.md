---
description: >-
  https://nextjs.org/docs/app/building-your-application/configuring/environment-variables
---

# Environment Variables

Next.js는 자체적으로 .env 파일들을 인식한다.

리액트에서 많이 사용하는 dotenv 라이브러리는 next-env에 내장되어 이미 사용되어져있음



serverside로 모든게 default 값이 되어 있는 Next.js는 env 역시 Node.js에서 실행이 된다.

고로 아무 설정 없이는 browser에서 env 가 작동하지 않는다.

그러므로 변수명 앞에  `NEXT_PUBLIC_` 를 작성해줘야 prefix를 인식해 brower에서도 작동을 시켜준다.&#x20;

### .env.local&#x20;

하나만 사용할 거면 이걸 사용.

default 값으로 세팅이 된다.

여기에 .env.development 와 .env.production 이 overwrite 되는 셈



### .env.development

yarn dev

### .env.production

yarn build

yarn start

### .env.test

test환경에서는 .env.local 이 default 값으로 실행되지 않음.
