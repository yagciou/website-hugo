---
title: "使用 hugo 在 GitHub 創建自己的 Blog"
date: 2021-03-18T17:22:18+08:00
draft: false
categories: ["Hugo"]
tags: ["hugo"]
---

### 1.安裝 Homebrew (以Mac為例)
##### 目前位置：~
`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`  
  
### 2. 安裝 Hugo
`brew install hugo`

### 3. 創建新網站
hugo new site 自己的網站資料夾名稱  
ex：`hugo new site yagblog-hugo`

### 4.進入剛創建好的資料夾 並 建立 git 數據庫
##### 目前位置：~
`cd yagblog-hugo`  
##### 目前位置：~/yagblog-hugo
`git init`

### 5. 選擇一個 [主題](https://themes.gohugo.io/) 並參考文件新增
這裡使用 fuji  
ex：`git submodule add https://github.com/amzrk2/hugo-theme-fuji.git themes/fuji`  
新增的主題會在 themes/主題名稱資料夾 ( 此處為 themes/fuji )

### 6. 複製並取代 static 和 layouts 資料夾
* 先移除 `yagblog-hugo` 資料夾裡的 static 和 layouts 資料夾
    ```
    rm -rf layouts 
     rm -rf static
    ```
* 再把 主題 裡的 static 和 layouts 資料夾複製過來  
    `cp -R ./themes/fuji/exampleSite/static static`  
    `cp -R ./themes/fuji/layouts layouts`
    
### 7. 在 /content/posts 建立新文章
hugo new posts/文章名字.md  
(文章名字可以用中文，但不可有空白否則會中斷)  
`hugo new posts/my-first-post.md`  

進入 /content/posts 資料夾就會看到 my-first-post.md 的 markdown 檔案，  
將 draft (草稿模式)改成 false 才會顯示文章。  
以後建立文章都是用此方式再去做修改。  

* 產生出的 md 檔案會長這樣子
```
---
title: "my-first-post"
date: 2021-03-19T12:20:11+08:00
draft: true
---
```
* title 可以空白
*  詳細屬性請參考下方 \"Hugo 支持的常用 Front Matter 屬性\"
* 可以修改 `archetypes/` 下的 `default.md` 預設模板來自製以後新增的初版 md 檔案

### 8. 複製並取代 config.toml
* 先移除 `config.toml` 檔案  
`rm -rf config.toml`  
* 再把 主題 裡的 config.toml 檔案複製過來  
`cp ./themes/fuji/exampleSite/config.toml config.toml`

### 9. 編輯 config.toml
修改以下三項，其餘版面設定依自己需求修改  
[官方配置文件](https://gohugo.io/getting-started/configuration/)


    baseURL = "https://GitHub帳號名稱.github.io/"
    languageCode = "zh-tw"
    title = "Yag Blog"    #網頁名稱，可自由命名

    
### 10. 本地測試網頁
`hugo server -D` (包含草稿)  
`hugo server` (不包含草稿)  

執行完後，在瀏覽器中輸入網址 `http://localhost:1313`，就可以看到網站。

## 部署到 GitHub
### 11. 在 GitHub 建立兩個 repository
在 GitHub 建立 yagblog-hugo 和 自己的GitHub帳號名稱.github.io 兩個repo。

### 12. 建立 /public 資料夾
##### 目前位置：~/yagblog-hugo
`hugo`

### 13. 將 /public 資料夾連結到 GitHub 上的 yagblog.github.io
##### 目前位置：~/yagblog-hugo
`cd public`
##### 目前位置：~/yagblog-hugo/public
```
git init
(git remote add origin 自己的GitHub帳號名稱.github.io 位置)
git remote add origin https://github.com/yagciou/yagciou.github.io.git 
git add -A
git commit -m "Initial commit"
git push -u origin master
```

* 接下來可能會讓你輸入你的 Github 帳號和密碼，之後就可以去 Github 和 http://帳號.github.io 查看是否成功。

### 14. 將整個 yagblog-hugo 資料夾連結到 GitHub 上的 yagblog-hugo
##### 目前位置：~/yagblog-hugo/public

`cd ../`
##### 目前位置：~/yagblog-hugo
```
git init
(git remote add origin 自己的GitHub上的yagblog-hugo 位置)
git remote add origin https://github.com/yagciou/yagblog-hugo.git
git add -A
git commit -m "Initial commit"
git push -u origin master
```

在執行 git add .時出現如下面的 warning 時不用在意

![示意圖](/images/hugo1.svg)

等個幾分鐘，去瀏覽器輸入網址 https://yagciou.github.io/ 就大功告成囉！

### 15. 更新 Blog 文章
##### 目前位置：~/yagblog-hugo

之後添加文章，只需要重新編譯 Hugo，重新提交到 Github 即可。  

```
hugo
cd public
```
##### 目前位置：~/yagblog-hugo/public
```
git add -A

建立新 commit 
git commit -m "本次更新的說明"
git push -u origin master
---------------------------------------------
不想建立新 commit 要使用合併
git commit --amend
git push -u origin master -f
```

`cd ../`
##### 目前位置：~/yagblog-hugo
```
git add -A

建立新 commit 
git commit -m "本次更新的說明"
git push -u origin master
---------------------------------------------
不想建立新 commit 要使用合併
git commit --amend
git push -u origin master -f
```


- - -

* 使用主題  
[fuji](https://github.com/dsrkafuu/hugo-theme-fuji/blob/master/README_CN.md)  
目前主題：  
[edidor](https://github.com/sfengyuan/edidor/blob/main/README-zh.md)

* 參考建置方式  
[參考建置方式 1](https://reurl.cc/zbKG76)  
[參考建置方式 2](https://chupai.github.io/posts/200316_hugo/)

* md檔案屬性與寫法  
https://markdown.tw/

    - 這是清單
    + 這也是清單
    * 這同樣是清單
        - 清單子項目
        
    1. 數字型清單
    2. 第二個數字清單
    2. 數字清單不需要連續數字
        3. 數字清單子項目
    
 **我是粗體**
 
 _我是斜體_
 
 *我也是斜體*

~~我被刪除~~
    
 ``只有一個 ` 可以轉換小段的程式碼``
 

    加入tab即可轉換程式區塊

```html
	<body>
	  <p>這是一段 HTML 結構</p>
	</body>
```

* 區塊引言  

> 可以在每個段落前方加上\>就行


* Hugo 支持的常用 Front Matter 屬性：  
    Front-matter 是 md 檔案最上方的分隔區域，用於指定個別檔案的變數。

    * title：標題名，使用 hugo new 建立會與檔名相同。  
    * date：日期，使用 hugo new 建立為目前時間。  
    * draft：草稿，如果是 true 生成網站時，不包括此頁面。  
    * description：內容描述，主要用於 SEO 優化。  
    * tags：標籤。  
    * categories：分類。  
    * keywords：關鍵字。  
    * url：文章 url 名稱，預設使用檔案名稱。  
    * weight：列表頁的文章排序，越小越靠前，無設定則依照時間排序。  
    
### 容易遇到的問題
* Markdown 圖片路徑  
在 Markdown 圖片路徑中，是以 `static/` 為根目錄寫全路徑。  
圖片位置：`/static/imgae/post1.png`，那麼在 Markdown 中寫作：  

`![圖片說明](/imgae/post1.png)`

