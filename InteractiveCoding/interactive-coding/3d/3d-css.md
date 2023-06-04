# 면 3D css 작업

앞면과 뒷면 개념을 가지기 (1F 앞 / 1B 뒤)

```markup
<div class="page">
    <div class="page-face">1F</div>
    <div class="page-face">1B</div>
</div>
```

이제 page를 하나의 면 set page-face를 각 앞과 뒤 면으로 생각.

```css
body {
  perspective: 1500px;
}
.leaflet {
  ...
  transform-style: preserve-3d;
  outline: 2px solid black;
}
.page {
  ...
  transform-style: preserve-3d;
  transform: rotateY(45deg);
  outline: 1px solid red;
}

.page-face:nth-child(2) {
  transform: rotateY(180deg);
}
```

### 3D 환경으로 속성 주기

만약 transform: rotateY(deg) 만 한다면 여전히 2D로 나올거다.

왜냐하면 전체 환경 자체를 3D를 하겠다라고 해줘야함.



그래서 body 가장 높은 곳에 perspective (관점) 속성을 주고

그 아래 태그들에게 고스란히 transform-style: preserve-3d; 속성을 처리해줘야한다.

\=> 해당 속성은 상속이 안일어남. 이렇게 일일히 적용시켜줘야한다.



### page-face div 태그 3D 하나의 면으로 움직이게 만들기

```css
.page-face:nth-child(2) {
  transform: rotateY(180deg);
}
```

이 코드가 page-face div 두개를 함께 움직이게 만들어준다.

이렇게 설정을 해놓으니  page-face div의 부모 태그인 page 의 transform 이 변경할때&#x20;

유기적으로 두번째 page-face div 태그가 움직이게 된다.





