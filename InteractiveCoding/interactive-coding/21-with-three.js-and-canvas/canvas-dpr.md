# canvas dpr 셋팅

![](<../../.gitbook/assets/image (1).png>) 맥 : dpr 2 / 그 외 다름



이게 dpr 이라고 해상도와 관련된 것&#x20;

dpr이 높으면 높을수록 해상도가 좋음



그러나 dpr이 2이상인 기기 또는 브라우저 등등에서는 이미 좋기에 별 차이가 없지만&#x20;

그 외의 것들은 시스템적으로 이걸 개선시켜놓아줄 수 있다.



방법은 간단.

1픽셀을 더 쪼개주면 됨.

대신 내가 원하는 값들과도 여전히 문제없이 일치시켜줘야하기 때문에&#x20;

```javascript
const dpr = window.devicePixelRatio;

const canvasWidth = 300;
const canvasHeight = 300;

canvas.style.width = canvasWidth + 'px';
canvas.style.height = canvasHeight + 'px';

canvas.width = canvasWidth*dpr;
canvas.height = canvasHeight*dpr;

ctx.scale(dpr, dpr)
```

결과적으로 다음과 같은 셋팅이 나오게됨.
