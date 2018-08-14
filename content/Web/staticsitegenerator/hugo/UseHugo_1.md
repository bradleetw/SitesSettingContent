---
title: "使用Hugo產生靜態網頁"
date: 2018-07-17T12:00:00+08:00
description: ""
tags: ["靜態網頁", "hugo"]
categories: ["Web"]
draft: false
authors: ["bradlee"]
---
## 為什麼要用靜態網頁產生器(Static Site Generators)?
靜態網頁產生器一般都會有很多現成的模板(template), 只要相關設定正確, 使用者只要專心編寫你的內容即可(但只要你有強迫症, 可能就會想要自己調整更多的細節).

原本我不知有這類的工具, 是因為在學習別的項目時看到別人的文章, 只用一兩句話描述說可以用Hugo很快產生網頁, 只要上網查找學習就可以, 然後我就上當了...

靜態網頁產生器這類工具確實可以很快產生網頁, 只要套一套現成模板, 輸入內容即可, 而且網路上也可以找到學習資源, 但是也可能因為使用這類工具太“簡單”, 相關的學習資源就沒有我預期的易懂, 所以我花了超乎預期的時間來了解使用Hugo.

## 下載安裝
可參考網路資源:
1. [在 Mac 上安装 Hugo](http://www.gohugo.org/doc/tutorials/installing-on-mac/)
2. [Hugo 官網](http://gohugo.io/getting-started/quick-start/)

我是透過 brew 下載安裝:

    $ brew install hugo

確認安裝結果:

    $ hugo version
    Hugo Static Site Generator v0.42.2 darwin/amd64

## 建立網站

    $ hugo new site MakeWebSite

hugo 會建立 MakeWebSite 目錄, 而且在這目錄底下產生 2 個檔案及 6 個目錄

    .
    ├── archetypes
    │   └── default.md
    ├── config.toml
    ├── content
    ├── data
    ├── layouts
    ├── static
    └── themes

## 下載模板
先依照官方 Quick Start 流程選擇 Ananke theme 這個模板, 在 [Hugo template 官網](https://themes.gohugo.io/)(應該是github) 有列出大家分享的模板, 初學者再挑選模板時除了挑好看之外也要注意該模板的 Readme.md 內容是否你看得懂, 因為有可能該作者預設你懂一些相關知識而沒有寫上, 而你調適的最後結果就是挫折滿滿.

透過 git 下載模板, 使用者可以先進到 themes 目錄中, 執行 git clone:

    $ cd themes
    $ git clone https://github.com/budparr/gohugo-theme-ananke.git ananke

下載完畢後, 要在 config.toml 中加入以下一行, 這個模板才會被套用上.

    theme = "ananke"

## 增加帖子

    $ hugo new posts/my-first-post.md

Hugo 會在 `MakeWebSite/content` 下創建 posts 目錄以及建立 my-first-post.md 這個檔案, 這就是你的第一個空帖子.

## 查看剛建立的網站
Hugo 本身提供 server 的功能, 可利用來檢視所建立的網站.

    $ hugo server -D

`-D`: 這個設定是讓 hugo server 可以列出還是草稿的帖子. (如何設定帖子是草稿還是完成品? 只要在編寫這些帖子檔案的開頭加上 draft: true. 這裡就開始有些東西要理解了, 不過我們放到後面的文章來說明)

利用瀏覽器看 http://localhost:1313/ 就可以看到所建立的網站了.

我相信使用者一定開始想客製化了, 後面的文章就將我想要的客製化其方法分享出來, 這篇的介紹就到這裡.
