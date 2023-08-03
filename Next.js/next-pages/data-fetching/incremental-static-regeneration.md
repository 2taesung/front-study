# Incremental Static Regeneration

증분 정적 사이트를 재생성한다.

\=> 재생성한다: (특정 주기로) 데이터를 가져와서 다시 그려준다.

\=> 증분 정적 사이트를 재생성한다: (특정 주기로) 정적인 사이트를 데이터를 가져와서 다시 그려준다.



ISR을 담당하는 함수는 getStaticProps로 동일한데 revalidate 옵션과 함께 할 뿐.

revalidate를 설정하면 next.js가 알아서 해당 주기마다 캐싱하고&#x20;





