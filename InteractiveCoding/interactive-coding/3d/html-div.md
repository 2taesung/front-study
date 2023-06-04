# html div 초기 셋팅

index.html

```markup
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="css/main.css">
</head>
<body>
  <div class="leaflet">
    <div class="page">
      <div class="page-face">1F</div>
      <div class="page-face">1B</div>
    </div>
    <div class="page"></div>
    <div class="page"></div>
  </div>
</body>
</html>
```

main.css

```css
html {
  font-size: 14px;
}

.leaflet {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  width: 30vw;
  height: 30vw;
  margin: auto;
  outline: 2px solid black;
}
.page {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
}
```



