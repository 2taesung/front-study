# CSS-in-JS

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



