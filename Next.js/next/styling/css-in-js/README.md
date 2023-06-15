# CSS-in-JS

<mark style="background-color:green;">기본적으로 CSS 방식은 정답이 없음.</mark>

이전부터 하시던 분들은 SCSS module 을 선호하는 것 같고,

css-in-js config가 불편하다 싶은 분들은 tailwind css 로 하는 것 같고

js 엔지니어링 자체를 좀 집중하는 분들은 js로 다 할 수 있는 css-in-js 스타일을 선호하는 것 같고



이런거를 해결(?), 짬뽕해서 시장을 잡고자 next.js에서 자체적으로styled-jsx를 만들음.

하지만 아직 정보, 장점, 기능 등이 확보되지 않은 상황에서 시장에서도 기존 css-in-js에게 밀리는 느낌.



### styled-jsx(next.js 기본제공)

Component를 이용해서 inline도 가능은 함

그러나 공식적으로 다양한 styled-jsx 기능 들을 Next에서 제공함.



가장 큰 장점은&#x20;

css 전염 => 정확한 명칭이 기억 안남.

<mark style="background-color:green;">component scope을 정해버리기 때문에 css 전염을 걱정할 필요가 없다.</mark>

심지어 이전에 죄악으로 여기던 html 기본 tag (div, span...)에 직접 style을 먹여도&#x20;

css 전염이 없기 때문에 문제 없다.



global은 또 global로 적용시키면 됨.



which unfortunately [do not support server-rendering and are JS-only](https://github.com/w3c/webcomponents/issues/71)

\=> 관련 링크의 내용을 이해 못함 ....

\=> 대략적으로 효율화를 시킬 수 있는 방법이 있을 것 같은데 scope으로 분리가 되었기 때문에

\=> 근데 아직이라는 말인듯 ...



관련 원리가 담겨있는 github

[https://github.com/vercel/styled-jsx](https://github.com/vercel/styled-jsx)



