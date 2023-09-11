# next/link

여러가지 a 링크에서 나아가 최적화가 되어있음

* <mark style="background-color:green;">prefetch</mark>로 routing 하기 전에 데이터 미리 가져옴
  * next.js의 getStaticProps 함수를 자체적으로 이용

\=> Link로 연결된 페이지 데이터들을 미리 가지고 들고 있는다.

* 동적 paths
  * dynamic route segments
  * URL Object



정확히 a tag와 Link 태그를 비교해보면

a는 html tag이기에 브라우저에서 실제로 이동하는 것을 액션함

새로고침과 함께 해당 페이지를 처음부터 끝까지 다 다시 실행함



하지만 Link의 경우 기존에 것에서 필요한 것들만 선택적으로 가져옴

이것을 <mark style="background-color:green;">Client Side Navigate</mark>라고 함.

실제 network를 비교해보면 Link는 한두개 a는 엄청 많이 발생.



또한 새로고침이 되기 때문에  a tag는 브라우저 상으로 핑크 배경을 주면 하얗게 새로고침 되는데 Link는 유지됨



### code spliting

원래next에서 auto spliting 최적화를 하는게 있는데&#x20;

얘네들이 link 태그가 등장하는 순간 prefetch를&#x20;



Viewport에 Link 컴포넌트가 노출되었을 때 href로 연결된 페이지의 chunk를 로드.

