# Week 9

* 중복을 가만 두지 마라&#x20;

axios, apiBaseUrl 을 모두가 알고 있을 필요가 없다.

이 raw한 단의 것을 하나로 묶어서 ApiService에서 숨겨준다.



axios 쓰겠지 내부적으로.

그런데 어느날 axios를 바꿔서 다른걸 쓰고 싶다?

하면 ApiService에서 한곳만 바꿔주면 된다.



* useEffect 의 의존성 배열의 기준

useEffect 안의 외부 영향주는 변수 전부 넣
