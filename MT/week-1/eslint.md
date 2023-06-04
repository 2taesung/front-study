# ESLint

&#x20; [**ESLint 공식문서**](https://eslint.org/)

* [린트](https://ko.wikipedia.org/wiki/%EB%A6%B0%ED%8A%B8\_\(%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4\))
* [정적 프로그램 분석](https://ko.wikipedia.org/wiki/%EC%A0%95%EC%A0%81\_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8\_%EB%B6%84%EC%84%9D)
* [Coding\_conventions](https://en.wikipedia.org/wiki/Coding\_conventions) \</aside>

무엇을 위해서?

* 스타일 통일
* 잠재적 문제 발견
* 베스트 프랙티스 추천 → 최신 트렌드를 학습하는데 활용할 수 있다.



.vscode/settings.json파일을 추가해 JS/TS 파일을 저장할 때마다 ESLint를 실행하고 문제점을 고치게 설정할 수 있다.

\=> vscode의 setting 전체를 건드리니까 최근에 기존에 멀쩡하던 코드에 lint 에러를 뿜어내기 시작했었음

\=> 내가 선택적으로 글로벌을 설정을 적절하게 하고 나머지는 이렇게 파일로 적용하는 것도 너무 좋은 방법인듯.



.eslintrc

```json
{
    "editor.rulers": [
        80
    ],
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    "trailing-spaces.trimOnSave": true
}
```

아래는 prettier 와 함께 하는 세팅.

```json
{
  "extends": ["react-app", "eslint:recommended"],
  "parser": "@babel/eslint-parser",// babel lint err
  "parserOptions": { "requireConfigFile" : "false" },// babel lint err
  "babelOptions": { "configFile": "./.babelrc" },// babel lint err
  "rules": {
    "no-var": "error", // var 금지
    "no-multiple-empty-lines": "error", // 여러 줄 공백 금지
    "no-console": ["error", { "allow": ["warn", "error", "info"] }], // console.log() 금지
    "eqeqeq": "error", // 일치 연산자 사용 필수
    "dot-notation": "error", // 가능하다면 dot notation 사용
    "no-unused-vars": "error" // 사용하지 않는 변수 금지
  }
}
```

### 사용하는VSCode extentions 정리

아샬님 추천 vscode extentions

[ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

\=> ESLint를 이미 설치도 했고 이걸 사용하려면

> npm run lint
>
> npm run lint --fix

등의 추가적인 작업을 해줘야한다.

\=> 그런데 이 extention을 이용하면 저장시 자동으로 반영해 고쳐줌.



[Trailing Spaces](https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces)

\=> 코드 이후에 있는 잔 공간들을 제거해줌



내가 추가적으로 애용하는 extention

[indent-rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow)

[markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)

