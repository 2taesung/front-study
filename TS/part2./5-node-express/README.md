# 섹션 5 - Node, Express

package가 없으면 index 체크



@types/node 같은 경우는&#x20;

declare module 이 있다.

이것은 특정 모듈의 선언임.



우리가 이전에 봤던 @types 들은 패키지 하나가 하나의 라이브러리의 type만을 담당했다.

그러나 @types/node 같은 경우는 이것저것 겹치는게 많다.



node 같은 경우는 뭔가 특별한게 아니라 js 런타임을 해주는거라고 보면 된다.

그러므로 js가 실제로 실행되는 환경인 browser랑 다르다.



msw 하면서도 이 차이점에 대해 알아본적이 있음.



여기서 또 차이가 확인되는데&#x20;

window 는 setTimeOut의 return 타입이 number(id)

node 에서는 setTimeOut의 return 타입이 NodeJS.Timeout(커스텀 객체)
