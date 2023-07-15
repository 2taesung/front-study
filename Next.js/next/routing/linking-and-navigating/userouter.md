# useRouter

기존의 React Router hook이랑 비슷한 api

우리가 알고 있는 history api 등을 동일하게 사용한다고 보면 됨.

push, refresh 등등...



### router.replace vs reuter.push

둘다history stack 해당 url을 stack 한다.&#x20;

그런데 replace는 현재 것을 대체하고 (이동한 후 전에거가 사라지고 그 전거만이 남아있다)

push는 그냥 말그대로 push 해서 쌓인다.



팁.

Link 컴포넌트와 다르게 연결된 페이지를 미리 불러오지 못함.

특정 상황이나 이벤트가 발생한 경우 클라이언트에서 사용자를 특정 페이지로 보낼때는 (로직)이 들어갈 때는 사용하기 좋으나 프레임워크인   Next.js의 힘을 쓰는 행위는 아님.



단테님 블로그의 하단에 실습까지 디테일한 설명 있다.

[https://velog.io/@jay/Next.js-13-master-course-routing-2](https://velog.io/@jay/Next.js-13-master-course-routing-2)
