---
title: 前端實作系列-上傳圖片並預覽
description: 讓使用者選取要上傳的圖片，並利用按鈕觸發預覽
date: 2022-06-18
categories:
    - HTML
    - JavaScript
    - 前端實作
tags : [
    "圖片上傳",
    "JavaScript"
]
---

很多前端工程師一定會使用到的功能：圖片上傳，並將圖片預覽在網頁畫面上，其實做法非常簡單

## 說明

- 利用 `input type='file'` 去取讓使用者選取要上傳的圖片
- 利用 `button onClick()` 觸發預覽圖片的funtion `fileUp()`
- 利用 `FileReader()` 讀出file資料
- 利用 `readAsDataURL` 產生出當下可用的URL供渲染網頁使用

## 程式碼

```html
<!DOCTYPE html>
<head>
  <meta charset="utf-8">
</head>
<body>
  <h3>實作檔案上傳預覽</h3>
  <input id="file1" type="file" accept="image/*" />
  <button id="btn1" onclick="fileUp()">預覽檔案</button>
  <p id="demo"></p>
  <div>
    <img id="img1" width="50%" />
  </div>
</body>

<style type="text/css">
  body {
    font-family: system-ui;
    background: #b3d9d9;
    color: white;
    text-align: center;
  }
</style>

<script>
  function fileUp() {
    const file = document.getElementById("file1").files[0];
    const reader = new FileReader();
    reader.onload = (e) => {
      const img = document.getElementById("img1");
      img.setAttribute("src", e.target.result);
      document.getElementById("demo").innerHTML = file.name;
    };
    reader.readAsDataURL(file);
  }
</script>
```

## GitHub Link
https://github.com/Yen-An/JS-

## Try in CodePen
https://codepen.io/yen-an/pen/poaGRRb