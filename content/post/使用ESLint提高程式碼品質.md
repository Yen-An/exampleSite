---
title: 使用ESLint提高程式碼品質
description: 在vscode中將ESLint、Prettier及Airbnb style guide結合。
date: 2022-08-08
categories:
    - Style Guide
    - JavaScript
    - ESLint
    - 前端實作
    - VSCode
tags : [
    "ESLint",
    "代碼風格"
]
---

## ESLint可以做什麼？

檢查出語法錯誤：變數未經宣告、function未經定義、括號不成對等等

將code格式化：如何縮排、單引號或雙引號、分號、space及tab的大小等等

刪除多餘的程式碼：提醒刪除import但沒有使用的模組、空的function、變數宣告但未使用等等

確保遵循最佳實踐：使用嚴格相等 `===` 而非 `==`



### 再搭配現在流行的 style guide：

- [Google](https://github.com/google/styleguide)
- [Airbnb](https://github.com/airbnb/javascript)
- [Standard](https://github.com/standard/standard)

透過以上兩種工具的結合，可以確保自己的程式碼與團隊遵循的規則相符，

一旦通過ESLint的代碼檢查，表示程式碼品質在一定的水準內。



## 在專案中引入ESLint套件

以下將會解說如何將vscode內的延伸模組Prettier與ESLint + Airbnb style guide做結合，

目標是禁用ESLint的格式規則，因為我們只需要用他來檢查語法錯誤，

並用Prettier格式化程式碼。

在開始之前，記得要先安裝 [npm](https://github.com/npm/cli) 及 [npx](https://github.com/zkat/npx)。

## 配置方法

1. 下載VScode的  [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) 及 [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) 延伸模組

2. 在我們的專案根目錄中安裝 ESLint 及 Prettier 套件

   `npm install -D eslint prettier`

3. 安裝 [Airbnb style guide](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb)

   `npx install-peerdeps --dev eslint-config-airbnb`

4. 安裝 [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)（禁用ESLint格式化）

   `npm install --save-dev eslint-config-prettier`

5. 安裝 [eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier)（允許ESLint在我們寫程式時顯示格式錯誤）

   ```
   npm install --save-dev eslint-plugin-prettier
   npm install --save-dev --save-exact prettier
   ```

6. 在專案根目錄建立檔案 .eslintrc ，內容如下：

```json
{
  "extends": ["airbnb", "prettier"],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": ["error"]
  },
}
```

最後，在vscode內設定格式化的工具為Prettier就好了，

設定的方式，可以在撰寫程式碼的地方，按右鍵>>格式化文件，

這時候vscode會跳出你要選擇什麼延伸模組去格式化，

在這邊選擇 Prettier 即可。