# tailwind css에 대한 기준

tailwind css는 기존의 bootstrap, MUI와는 다르다.



css 프레임워크라고도 표현하는데

css 라는 <mark style="background-color:green;">raw한 단계</mark>의 style sheet language에 <mark style="background-color:green;">하나의 추상 레이어</mark>를 쌓아 올려&#x20;

그렇게 쌓아 올려진 레이어 (class)를 사용하는 것이다.



기존의 bootstrap, MUI 같은 경우는 기존의 css를 활용해 컴포넌트 단위로 만들어져 있어 사용하는 것이지 tailwind css는 css들을 조합해서 tailwind css라는 라이브러리가 탄생한 것이다.



이것으로 인해 생기는 장단점들이 존재한다.

장점

1. 디자인 고효율을 뽑을 수 있다.

인력, 시간이 없는 상황에서 누군가 만들어놓은 class들을 사용할 수 있다.

2. 디자인에 적용 유연성 문제 없음

아무래도 tailwind css 정도 검증된 프레임워크라면 디자이너, 기획자가 제시하는 디자인까지 개발이 진행되는데 문제 없다라고 생각해도 좋다.



단점

1. 신입 개발자 학습 진입장벽

만약 tailwind css를 모르는 개발자가 왔을때 해당 시스템을 추가 학습해야함

2. tailwind css 버전, 업데이트 등을 계속 추적해야함(팔로우업)

tailwind css는 매일매일 업그레이드가 된다.

그러므로 tailwind css를 도입했다면 해당 버전, 업그레이드를 매일매일 체크해야한다.

드문 경우겠지만 버전이 어긋나거나 이전에는 지원했다가 현재 하지 않는 등의 문제로 버그가 발생할 수 있다.

