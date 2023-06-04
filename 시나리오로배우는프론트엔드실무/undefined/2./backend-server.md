# 기본 Backend server 셋팅

nest.js

{% embed url="https://nestjs.com/" %}

### dist 폴더

프론트엔드와 같은 dist 폴더의 존재는 ts 때문



### MVC 패턴

Model / View / Controller

이 세가지로 분리되어 있는 디자인 패턴

(대표적으로 spring)



View는 프론트엔드에서 할거니까 api로 보내고

Model은 'entity' 에 해당

Controller는 entity에서 api를 제공하는 부분&#x20;



### ORM

프론트엔드가 데이터를 api를 통해 받아온다고 하면 백엔드도 결국 데이터를 어디선가 가져와야하는데 가져오는 장소는 바로 database



그리고 rdbms라면 sql문법을 통해 가져올 수 있다. 우리가 이해하기 쉽게 비유해보자면 프론트엔드 개발 역시 html, js 가 버무러져 있으면 개발하기 어렵다.



그래서 벡엔드에서도 sql문과 코드들이 섞여 있으면 상당히 피로도도 있고 어렵다. 개발자들이 이 data를 코드 레벨에서 관리하고 다루고자 했고 그렇게 탄생한 소프트웨어가   orm이다.

이 orm을 이용하면 data를 javascript 객체 또는 typescript 객체를 다루듯이 하면서 이것을 자연스럽게 코드에 버무릴 수 있다.

\=> ORM의 필요성을 이렇게 설명하니 굉장히 이해가 잘됨.



Typescript 데코레이션 기능

<mark style="background-color:orange;">이건 잘 모름</mark>



### RDBMs

RDB는 데이터들간의 관계를 1대1 1대다 다대다의 관계를 설정할 수 있다.

\=> 장고 했을때 기억이 새록새록.



### swagger를 통해 자동으로 api 문서를 만들 수 있음

swagger를 통해 ApiResponse, ApiOperation, ApiTags 들 존재.

기본적으로는 벡엔드가 프론트엔드와 상의해서 api 문서를 만들어주는게 일반적.



이 api 문서가 있냐 없냐가 프론트엔드 입장에서도중요하다.

```bash
npm run start:debug
```



\=> 기본적인 벡엔드 코드를 다루는건 내가 생각해도 필요(왜냐하면 나는 할 줄 아니까)

﻿
