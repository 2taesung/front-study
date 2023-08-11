# 섹션 0. 기본 세팅하기

### 타입스크립트를 할 때 알아야 할 단 한가지

> ### ts는 최종적으로 js로 변환된다.

### 기본지식

* ts에서는 말이 되는데 js에서 말이 안되는 코드는 있을 수 없
* 브라우저, 노드는 모두 js 파일을 실행함. (ts 모름)
* tsc라는 컴파일러가 컴파일로 js로 바꿔줌
* tsc는 tsconfig.json(tsc --init 시 생성)에 따라 ts 코드를 js(tsc 시)생성 바꿔줌
* 인풋인 ts와 아웃풋인 js 모두에 영향을 끼침으로 tsconfig.json 설정 반드시 봐야함
* tsc가 하는 역할은 대표적으로 두가지 1. js로 변환 2. 타입체크&#x20;
* 타입에 에러가 발생하더라도 js로 변환은 진행됨 왜 ? 타입이 없더라도 js로서는 문제없는 코드
* ts 파일을 실행하는게    아니라 결과물인 js를 실행해야함
* editor(vscode, webstorm)가 필수. 왜냐하면 editor에서 런타임으로 타입을 체크해줌 안그러면 npx tsc --noEmit으로 그때그때 타입을 체크해야



### tsc 설치 - [MT tsc 설치와 비교해보기](http://127.0.0.1:5000/s/XcE6iWlyTypdRBbfFkCR/week-1/undefined#typescript-+-react-+-jest-+-parcel)

> tsc --noEmit&#x20;

\=> 노애미가 아니라 노이밋을 하면 단순 타입 검사할 때 많이 씀



### tsconfig.json

npx tsc --init 시에 기본 설정

```json
{
  "compilerOptions": {
    "target": "es2016",
    "module": "commonjs",
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "skipLibCheck": true
  }
}
```

추가 변경 설정

```json
{
  "compilerOptions": {
    "allowJs": true,
    "jsx": "react-jsx"
  }
}
```

<mark style="background-color:orange;">=> allowJs 옵션이 정확히 필요한 것일지 재고가 필요</mark>

