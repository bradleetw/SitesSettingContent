---
title: "透過調整 config.toml 設定 Hugo 網站(1)"
date: 2018-07-17T15:10:22+08:00
description: ""
tags: ["靜態網頁", "hugo"]
categories: ["Web"]
draft: false
cover:
    image: /images/beach-beautiful-view-cliff-1249004.jpg
    style: wide
authors: ["bradlee"]
---
## 透過合適的模板來學習調整 Hugo 網站
一般來說在 GitHub 上的每一個模板除了使用說明檔(Readme.md)之外, 也會附上如何使用的範例, 例如你可以在 `themes/ananke/exampleSite` (ananke 換成你所下載的模板名稱)中看到相關的使用範例, 透過這些也可以很快上手 Hugo 網站的調整設定. 不過我也下載過很多沒附上 exampleSite 的模板, 而且Readme.md 也不是寫給初學者看的, 造成學習上的難度. 所以初學者挑選學習的模板請謹慎.
官方 Quick start 中所用的模板 [ananke](https://github.com/budparr/gohugo-theme-ananke.git) 就涵蓋這些資料.

## config.toml
Hugo 網站主要是透過 config.toml 這個檔案來調控, 當你透過 `$ hugo new site YourWebSite` 建立空網站時 Hugo 就幫你建立一個 config.toml (也支持 yaml 和 json 格式, 預設是 toml 格式).

直接先用所下載模板提供的 config.toml, `themes/ananke/exampleSite/config.toml` 取代原本 `config.toml`, 了解一下模板的 README.md, 再來更改相關的欄位.

1. 先移除 `themesDir = "../.."` 這行.

2. title = "Your new Hugo Site Title"

    這欄位的文字通常是呈現在你的首頁.
3. theme = "ananke"

    這欄位填入你所選用的模板名稱, 但請注意, 有時候你下載的目錄名會和 github 上列的名稱不一樣, 要以你這個模板的目錄名稱為主.
4. Paginate = 5

    這是決定你的列表一次可以列出幾個貼子的鏈結.
5. 在 [params] 區段中有幾個社交網站的欄位, 你可以填入你個人的相關帳號, ananke 這個模板在這個部分比較不友好, 你必須填入完整的 url, e.g. https://www.facebook.com/yourfacebookaccountname .

6. [params] featured_image = "/images/yourHomeSiteImages.jpg"

    ananke 這個模板可以讓你變更主頁的背景圖. 請先在你所建立網頁目錄的 `/static` 中建立 images, 並放入圖檔, 然後在 config.toml 中更改 featured_image 這個欄位的資料.

這些簡單的步驟, 就可以很快改出特別風格的網頁(其實只要換一張圖你就會覺得改很多... ).

待續...
