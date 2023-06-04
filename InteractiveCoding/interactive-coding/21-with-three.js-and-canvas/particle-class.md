# Particle class

```javascript
class Particle {
  constructor(x, y, radius) {
    this.x = x;
    this.y = y;
    this.radius = radius;
  }

  draw() {
    ctx.beginPath()
    //custom
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI / 180 * 360);
    ctx.fillStyle = 'red'
    ctx.fill()
    ///
    ctx.closePath()
  }
}
```

animate 함수

```javascript
// custom
const x = 100;
const y = 100;
const radius = 50;
//
const particle = new Particle(x, y, radius)

function animate() {
  window.requestAnimationFrame(animate)

  //겉으로는 표가 나지 않지만 전체를 지운다.(심지어 부분 지우는 것도 가능하다)
  ctx.clearRect(0, 0, canvasWidth, canvasHeight)
  particle.draw()
}

animate()
```

animate 함수는 window.requestAnimationFrame(animate) 재귀를 통해 계속 반복해서 실행되도록 만들었다. (console.log(1)을 찍어보면 계속 올라감)

이를 통해 실제로 애니메이션을 만들듯 프레임을 만들어내는셈.

[ctx.clearRect](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/clearRect)
