# 메소드와 this 타이핑

이제 $("p").<mark style="background-color:green;">removeClass("myClass noClass")</mark>.addClass("yourClass");



```typescript
removeClass(className_function?: JQuery.TypeOrArray<string> | ((this: TElement, index: number, className: string) => string)): this;
```

여기서 JQuery.TypeOrArray\<string> ?



```typescript
declare namespace JQuery {
    type TypeOrArray<T> = T | T[];
```

뜯어보기 팁으로 이렇게 밝혀진건&#x20;



removeClass(className\_function?: <mark style="background-color:green;">string | string\[]</mark> | ((this: TElement, index: number, className: string) => string)): this;

이렇게 써버리는 것이 추적하기 좋음.

\=> 이렇게 우리가 타입을 보면서 알게되는 좋은 점은&#x20;

\=> removeClass함수의 인자로 string\[]도 들어갈 수 있다는 점.



### &#x20;this 타이핑

this는 알다시피 js에서 약간 특수한 문법이다.&#x20;

이 this는 모든 js function 들에 예외처리를 해야하는 부분이다.&#x20;

고로 this는 일반적인 경우에는 쓰이지 않는다.



removeClass(className\_function?: <mark style="background-color:green;">string | string\[]</mark> | ((index: number, className: string) => string)): this;



지워버려.

점점 단순해지고 있다.



그럼 여기서 removeClass의 결과값이 뭐길래 . 일명 chaining이 가능한가?

removeClass의 결과값은 this&#x20;



this는 이전 거인 $("p") 이다.

그렇기 때문에 $("p").removeClass("myClass noClass").addClass("yourClass");

$("p").<mark style="background-color:green;">addClass("yourClass")</mark>;

이렇게 넘어간다.













