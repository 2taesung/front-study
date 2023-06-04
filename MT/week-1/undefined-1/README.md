# 번들러(빌드)

번들러 : 여러 개의 파일을 모듈화 해서 하나의 파일로 묶어주는 도구.



번들러는 브라우저에서 ESM(ES Modules)을 지원하기 전, JS 모듈화를 Native 레벨에서 진행할 수 없었음. 따라서 "번들링(Bundling)"이라는 우회적인 방법을 사용.



그래서 번들러의 핵심 목적은&#x20;

* ts, jsx, tsx 등 -> JS로 트랜스파일링
* 플러그인 추가
* 폴리필(Polyfill) 적용(Babel, SWC의 역할이 포함되어버림)

[Parcel vs Rollup vs Webpack 비교](https://velog.io/@subin1224/Parcel-vs-Rollup-vs-Webpack-%EB%B9%84%EA%B5%90)

\=> Webpack의 문제점을 인식해 다른 애들이 나옴

\=>  각각의 장단점들이 있어 적절한 상황에 적용이 베스트결론.



최신 트렌드는 번들링(빌드) 속도가 왜이렇게 오래걸리냐&#x20;

속도를 빠르게 개선해서 개발 경험을 향상시키자

그런데 기본적으로 번들링의 작업들이 NodeJS 싱글 스레드 구조다 보니 한계 존재.



그래서 Native 영역에서 성능을 높임

* Golang -> [esbuild](https://esbuild.github.io/) (안정성 높음)
* Rust -> [SWC](https://github.com/swc-project/swc)

[SWC를 개발한 한국인 특강](https://www.youtube.com/watch?v=4RJxyGJQe4o)

여기에이들을 이용해 Node.js로 한단계 래핑 및 활용하여 속도를 개선

* esbuild -> Vite, Snowpack





[Webpack → Vite: 번들러 마이그레이션 이야기](https://engineering.ab180.co/stories/webpack-to-vite)

[직접 webpack, babel 설정 잘 설명되어있는 글](https://juni-official.tistory.com/158#3.-%EB%B0%94%EB%B2%A8babel)



