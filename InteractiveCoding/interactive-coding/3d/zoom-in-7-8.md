# zoom in #7 #8

클릭했을때 중앙으로 클릭한 컨텐츠로 와야하고 사선으로 있는 page-face는 맞는 angle로 돌아와야함.

해당 컨텐츠만 보이고 나머지는 안보이고 back 버튼 역시 없다가 생김



html에 각 페이지에 1,2,3 특정할 데이터 속성 추가

```html
<div class="page" data-page="1">
```



main.js의 zoomIn 함수

```javascript
let currentMenu;

function zoomIn(elem) {
  const rect = elem.getBoundingClientRect();
  const dx = window.innerWidth/2 - (rect.x + rect.width/2);
  const dy = window.innerHeight/2 - (rect.y + rect.height/2);
  let angle;

  switch (elem.parentNode.parentNode.parentNode.dataset.page*1) {
    case 1:
      angle = -30;
      break
    case 2:
      angle = 0;
      break
    case 3:
      angle = 30;
      break;
  }
 
  document.body.classList.add('zoom-in');
  leaflet.style.transform = `translate3d(${dx}px, ${dy}px, 50vw) rotateY(${angle}deg)`;
  currentMenu = elem;
  currentMenu.classList.add('current-menu');
}
```

\=> 우리는 지금 x, y, z, angle 전부 내가 클릭한 list의 좌표에 따라 다르게 이동시켜주어야한다.

\=> getBoundingClientRect를 사용하면 내가 클린한 부분의 좌표 데이터들이 예쁘게 나온다.

{% hint style="info" %}
left, right / x, y 둘이 브라우저에따라안나오고 나오고가 있는 경우가 있음
{% endhint %}

\=> 해당 수식들은 강사님이 계산 값.

\=>  switch 문 안의 \*1 은 문자열로 나오는 값을 숫자로 바꿔줌(몰랐는데 가장 쉬운 방법이겠네;)



\=>높은 위치( body.classList)에서  zoom-in class 를 추가하고  click 한 elem는 currentMenu 전역 변수에 담는다.

\=> 이에 따라 css도 적



main.css에&#x20;

leaflet class에 transition 속도 지정

```css
.leaflet {
  ...
  transition: 1s;
}
.menu-item {
  ...
  transition: 0.5s;
}
.zoom-in .menu-item {
	opacity: 0;
}
.zoom-in .menu-item.current-menu {
	opacity: 1;
}
```

\=> 이로써 클릭한 친구 외로 menu-item은 opacity가 0이됨.



