# styled-components 설치

```sh
npm i styled-components
npm i -D @types/styled-components @swc/plugin-styled-components
```



### .swcrc 파일 작성

SSR 지원 등 Babel Plugin을 SWC에서 쓸 수 있도록 포팅

우리가 현재 쓰는 Parcel에서는 자동으로 SWC를 지원한다.

```json
{
	"jsc": {
		"experimental": {
			"plugins": [
				[
					"@swc/plugin-styled-components",
					{
						"displayName": true,
						"ssr": true
					}
				]
			]
		}
	}
}
```





