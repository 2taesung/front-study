# getStaticProps(SSG)

dev 서버 환경에서는 ssr처럼 작동한다.&#x20;

build를 해서 체크해야 제대로 동작함.



적용 여부 선택 기준 : 사용자가 페이지를 요청하기 전에 pre-render 할 수 있는가?

Yes라면 효율성 등을 고려했을 때 적용.



SSG를 사용하면 좋은 페이지들

* Marketing pages
* Blog posts
* E-commerce product listings
* Help and documentation



SSG의 2가지 케이스

* 외부 데이터 없이 pre-rendering
* 외부 데이터를 가져와서 pre-rendering





