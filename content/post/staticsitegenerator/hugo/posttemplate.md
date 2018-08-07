---
title: "[Hugo]建立固定格式的新帖子"
date: 2018-08-01T13:09:33+08:00
draft: false
tags: ["static-site-generator", "hugo"]
categories: ["Web"]
featured_image: "/images/paper-3042645_1920.jpg"
description: ""
author: "Brad Lee"
---
## 創建固定欄位的 Markdown 檔案

當使用者在一般的文書編輯器要開始創立 Markdown 新文章時, 除了透過該編輯器的 new file 外, 好像就沒有其他方法, 而這種方式只能產生一個空的檔案. 所以我們目前只能用 command line 來透過 `$ hugo new newPostFile.md` 的命令來產生新的 markdown 文章, 而且該文章會自動生成固定的欄位, 方便使用者寫作.

## 為什麼要透過這種方式來創建 Markdown 文章

透過這種方式, 使用者可以事先將 Markdown 文章常用到的 metadata 的欄位或者該欄位的值放到特定檔案, 在創建新 Markdown 文章時就能預設有這些欄位, 節省使用者寫作時間.

## 修改 **default.md**

當使用者透過 `$ hugo new newPostFile.md` 時, Hugo 會到該 Hugo project 底下的 `archetypes` 目錄找尋 `default.md`, 依據其內容而在新的 Markdown 檔案產生相對的欄位. 一般來說在 GitHub 上所公開的模板可能也會附上相對的 `default.md` (其實很多也都沒附上), 使用者只要下載該模板後, 到該模板的目錄下找 `archetypes` 就可以發現.

透過 `$ hugo new site newProject` 產生網站時, 會生成 `default.md` , 內容如下:

    ---
    title: "{{ replace .Name "-" " " | title }}"
    date: {{ .Date }}
    draft: true
    ---
目前我使用的經驗會再加上以下的資料:

    tags: []
    categories: []
    author: "Your Name"

以下是我目前使用的 default.md :

    ---
    title: "{{ replace .Name "-" " " | title }}"
    date: {{ .Date }}
    draft: true
    tags: []
    categories: []
    featured_image: "/images/yourimagebackgroundfilename.jpg"
    description: ""
    author: "Brad Lee"
    ---
    ## WHAT

    ## WHY

    ## WHERE

    ## WHO

    ## WHEN

    ## HOW

    ## HOW MUCH

修改完 `default.md` 後, 每次創建新 Markdown 文章時就可以有固定的格式.

## 題外話

這裡產生一個新問題, 我所用的 Atom 是否有 plug-in 可以產生 Markdown file? 待續 ...

(更新) 透過 atom install packages 中搜索 hugo ,找到了 3 個:

1. **language-hugo**:

    用途: Adds syntax highlighting to Hugo files in Atom. 若使用者在開發模板的時候, 在編寫 html 時, 會將相關的 keyword 區隔出來.

    目前版本: 0.5.1, 最後更新日期: 2018/03/15, 下載量: 2,552

2. hugofy:

    用途: 功能不完善, 且只有上一次代碼, 可以直接忽略.

    目前版本: 2.0.0, 最後更新日期: 2017/02/16, 下載量: 1,369

3. **atom-hugo**:

    用途: 可以在 atom 中直接創建 hugo 用的 Markdown file, 看了一下代碼, 就等同於在 command line 中執行 `$ hugo new newFile.md`. 這應該就是我所想到問題的解答. 這個 plug-in 還提供了其他功能, 如: 建立準備部署的網站, 執行 hugo server 等, 但是, 卻無法將 `baseURL` 變更成使用者想要的, 導致這些功能產生的網頁都指向錯誤的網址. 所以這個 plug-in 只剩建立新文章及建立網站架構這 2 個功能可用, 老實說, 這樣不如直接在 command line 自己創建一些 script 來得實用.

    目前版本: 0.1.2, 最後更新日期: 2018/03/13, 下載量: 458

題外話問題的結論: 直接在 commnad line 建立 script file.
另外, 有找到一個 plug-in, markdown-writer, 看起來功能還蠻多, 下載的人數高達 38 萬, 可惜沒支持 hugo.
