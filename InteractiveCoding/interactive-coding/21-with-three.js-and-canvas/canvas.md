# canvas 셋팅

### 캔버스 사이즈 이해하기

default 값은 300 \* 350

```markup
<body>
  <canvas></canvas>
  <script type="module" src="./index.js"></script>
</body>
```

```javascript
const canvas = document.querySelector('canvas');

console.log(canvas)

const ctx = canvas.getContext('2d');
console.log(ctx)

ctx.fillRect(10, 10, 50, 50)
```

canvas 사이즈를 다루는 두가지 방법이 있음음

### css 값을 직접 지정

```javascript
canvas.style.width = 300 + 'px';
canvas.style.height = 300 + 'px';

ctx.fillRect(10, 10, 50, 50)
```

이 방법은 canvas 객체 를 둘러싼 css의 값을 처리하는 거기 때문에&#x20;

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

의도치 않게 canvas 내부의 값들에도 영향을 끼치게 된다.

그 이유는 어거지로 외부의 속성 값을 바꿔버리기 때문에 내부의 것들도 강제로 끌어댕겨져버림.



### canvas 자체의 속성 값 지정

```javascript
canvas.style.width = 300 + 'px';
canvas.style.height = 300 + 'px';

canvas.width = 300
canvas.height = 300

ctx.fillRect(10, 10, 50, 50)
```

그래서 이렇게 자체 값과 속성 값을 동일하게 맞춰주어야함 => 정상 작동



만약, 이 값을 다르게 준다면 ?

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

이렇게 화질이 깨지게 됨.



고로 우리는 최종적으로

```javascript
const canvasWidth = 300;
const canvasHeight = 300;

canvas.style.width = canvasWidth + 'px';
canvas.style.height = canvasHeight + 'px';

canvas.width = canvasWidth
canvas.height = canvasHeight
```

고로 이 둘을 맞춰주기 위해 변수하나로 사이즈관리.
