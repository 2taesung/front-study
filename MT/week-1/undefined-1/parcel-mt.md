# Parcel(mt)

[Parcel 공식문서](https://parceljs.org/)

**Zero Configuration**

* 특별한 설정 없이 바로 사용 가능한 빌드 도구.&#x20;

\=> 공식문서 보면 제목도 Zero Config라고 대문짝만하게 어필

* [<mark style="background-color:green;">내부적으로 SWC를 사용해</mark>](#user-content-fn-1)[^1] 기존 도구보다 빠르다(ES Module을 적극 활용하는 Vite도 엄청나게 빠름).
* 참고:
  * [https://github.com/ahastudio/til/tree/main/parcel](https://github.com/ahastudio/til/tree/main/parcel)
  * [https://github.com/ahastudio/til/tree/main/vite](https://github.com/ahastudio/til/tree/main/vite)

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>



설정이 필요 없다고 했지만, 다음 두가지 작업은 하는 게 좋다.

### `1. package.json` 파일에 source 속성 추가.

```
"source": "./index.html",
```

\=> 이미 되어있긴 함. 체크하자.

\=> 만약 이걸 안하고 parcel을 실행시키면 에러가 발생

> npx parcel index.html
>
> 한 후
>
> npx parcel index.html --port 8080&#x20;
>
> 추가

### 2. parcel-reporter-static-files-copy

[parcel-reporter-static-files-copy](https://github.com/elwin013/parcel-reporter-static-files-copy) 패키지 설치 후 \`.parcelrc\` 파일 작성. 이렇게 하면 static 폴더의 파일을 정적 파일로 Serving할 수 있다(이미지 등 Assets).

```json
{
  "extends": ["@parcel/config-default"],
  "reporters":  ["...", "parcel-reporter-static-files-copy"]
}
```

\=> 귀찮지만 parcel은 이 기능을 지원 안해주는 듯.&#x20;

<mark style="background-color:orange;">=> 구체적인 이유나 로직 원인 공부 및 질문</mark>&#x20;



### 빌드 + 정적 서버 실행

> npx parcel build
>
> or
>
> npx servor ./dist

\=> servor 오타 아님 zero config라는 의도에서 o ㅋㅋ

\=> 이건 이런게 있다 정도 안되는 기능이 많음&#x20;



<mark style="background-color:orange;">dist 파일의 정체에 대해서 정확히 공부하자</mark>

### dist 폴더를 지우는데 겁낼필요 없음

run 해도 자동으로 만들어짐  등 의도치 않게 생길 수 있음

build할 때 마다 겹쳐써짐

\=> 고로 build 하기 전에 다 지우고 다시    해줘도 좋음





















[^1]: SWC를 추가적으로 설치할 필요 없다.
