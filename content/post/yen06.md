---
title: 前端實作系列-在React Project內串接第三方API
description: 在React Project內串接第三方API，以政府開放資料為例。
date: 2022-06-20
categories:
    - React
    - JavaScript
    - API
    - 前端實作
tags : [
    "政府開放資料",
    "第三方API串接"
]
---


很多時候我們會需要去串接第三方API，而我的習慣是，在真正去project call api之前，會用postman先測試過，那天心血來潮去試著call 政府的 open data ，用的是

[全國街道路名]: https://od.moi.gov.tw/api/v1/rest/datastore/301000000A-000917-035

的api，



在postman的結果，很正常，

![image-20220620112657719](/Users/yanlaoan/Library/Application Support/typora-user-images/image-20220620112657719.png)



於是我在我的React Project寫下fetch

```javascript
  fetch("https://od.moi.gov.tw/api/v1/rest/datastore/301000000A-000917-035")
  .then((res) => console.log(res))
```

結果出現了錯誤訊息，上面寫的要在我們發送請求時加上 `mode:'no-cors'`

![image-20220620113142449](/Users/yanlaoan/Library/Application Support/typora-user-images/image-20220620113142449.png)

於是我加上了

```js
  fetch("https://od.moi.gov.tw/api/v1/rest/datastore/301000000A-000917-035",{
  mode:'no-cors'
  })
  .then((res) => console.log(res))
```



But!!!!!人生就是這個BUT!!!!!!!

![image-20220620113803587](/Users/yanlaoan/Library/Application Support/typora-user-images/image-20220620113803587.png)

可以看到我的 Response 裡面有個 `type ='opaque'`，關於這個錯誤大家可以上網查查，簡單來說，這是一個不透明的 response，我們是無法去取得裡面的資料，所以 body 裏面是 null，事實證明 `mode='no-cors'`  並不會讓事情成功的執行，



我也有試過什麼setupProxy，依舊無法取得我想要的資料，



就在想要放棄之際，我看到了一個東西，

https://chrome.google.com/webstore/detail/allow-cors-access-control/lhobafahddgcelffkeicbaginigeejlf/related?hl=en

這是google chrome的一個插件，可以允許跨域請求，



我將他安裝在我的瀏覽器，並按下左下角的toggle on ，

![image-20220620120541439](/Users/yanlaoan/Library/Application Support/typora-user-images/image-20220620120541439.png)



然後回到我的程式碼，將 `mode:'no-cors'` 拿掉，再去到開發者工具看看這次回傳什麼，

![image-20220620120935256](/Users/yanlaoan/Library/Application Support/typora-user-images/image-20220620120935256.png)

可以看到我的 Response type 已經是 cors，但body依舊怪怪的？沒有我要的data，

接著我利用插件的 Test Cors來檢查我的瀏覽器到底可以接受怎樣的跨域請求，

![image-20220620121125924](/Users/yanlaoan/Library/Application Support/typora-user-images/image-20220620121125924.png)

可以看到我的fetch通通都是被拒絕的，但是，XMLHttpRequest的 GET & POST都是被允許的，

![image-20220620121206852](/Users/yanlaoan/Library/Application Support/typora-user-images/image-20220620121206852.png)



於是我將我的 fetch 改成 axios，因為axios的請求格式就是 XMLHttpRequest，

```js
  axios.get("https://od.moi.gov.tw/api/v1/rest/datastore/301000000A-000917-035")
  .then((res) => console.log(res))
```

讓我們再回到開發者工具看看，

![image-20220620121608868](/Users/yanlaoan/Library/Application Support/typora-user-images/image-20220620121608868.png)

這次成功的回傳了api所提供的data!!!!!



以上就是我在react project 直接去串接第三方api的辦法，供大家參考。

