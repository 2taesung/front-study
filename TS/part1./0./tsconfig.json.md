# tsconfig.json 상세 옵션 설명

```json
"allowJs": true 
```

\=> js와 ts를 함께 공존하게 하게는 옵션

\=> js에서 ts를 옮긴다거나 아직 ts 가 능숙하지 않을때 둘을 공존시킬때 유리



기본세팅 옵션들--------------------------------------------&#x20;

```json
"strict": true
```

\=> ts 어렵다고 false로 하는 사람 있는데 이럴거면 ts 쓰지마

```json
"esModuleInterop": true
```



```json
"target": "es2016"
```

\=> ts가 es2016버전의 js로 바꿔준다는 뜻

```json
"module": "commonjs"
```

\=> node.js에서는 모듈 시스템들이 많은데 그것들 중 선택하는 것.

<mark style="background-color:green;">=> 모르겠다.</mark> => 조현영님께 질문을 드렸고 답변 받음

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

```json
"forceConsistentCasingInFileNames": true
```

\=> 파일의 대소문자를 강제로 지정하는 룰

\=> 모듈 시스템이 있어서 다른 파일들을 import 해올 수 있다.

\=> 근데 파일의 대소문자를 윈도우에서는 구별 잘 않는다.

\=> 그러나 맥, 리눅스에서는 에러가 발생



```json
"skipLibCheck": true
```

\=> 라이브러리들에서 .d.ts file이 수도없이 많이 있음

\=> 이것들을 compile 할때 다 하면 오래걸리고 비효율적이니 실제로 쓰는      애만 check 하겠다는&#x20;
