---
title: "如何利用 GitHub Pages 建立博客?"
date: 2018-07-19T14:31:14+08:00
draft: false
description: ""
tags: ["GitHub", "deployment"]
categories: ["Web"]
authors: ["bradlee"]
---
## 什麼是 GitHub Pages(blog)?
在大家的印象中 GitHub 只是一個利用 git 讓大家免費放代碼, 追蹤 issues , 和各地好手討論的地方. 某天看到ㄧ篇文章的 URL 很特別, 是 https://xxxxxx.github.io/ , 和我平常看 GitHub 的 https://github.com 很像, 後來才知道 GitHub 可以讓使用者在上面放 blog(有空還是要看看人家的 "Read the guide"), 重點是"不用錢"(廢話, 不過被微軟買掉後會不會調整, 就不知了).

refer to: [What is GitHub Pages?](https://help.github.com/articles/what-is-github-pages/)

## 為什麼要使用 GitHub 來架設 blog?
在嘗試 GitHub 架設 blog 之前, 我正在學習使用 Google Cloud platfrom 試著架設 blog 網站, 自己申請域名, 申請 SSL, 突然想起 GitHub 上也有 blog 功能而且我也還沒試過, 查了一下, 還蠻容易設定的, 而且省去申請域名, SSL, 不用擔心服務器防火牆的相關問題, 當然你必須要有 GitHub 帳號(廢話 ~). 所以使用可以先用 GitHub 來放你的第一個 blog, 當然還有很多地方也有這類的功能, 如 medium, wordpress, 有空也來試試.

若你的網站不用利用 PHP, Python, or Ruby 來動態生成網頁, 只是個單純的靜態網頁(static site), 你就可以來使用 GitHub Pages.

GitHub Pages 分成兩類:

1. **User and Organization Pages sites**:
若是為了個人博客, 或是組織網頁, 就可以採用這個方式, 使用非常簡單.

2. **Project Pages sites**:
當要為了專案進行介紹說明, 可以採用這方式架設 GitHub Pages, 相關網站的檔案都是和專案的代碼或檔案放在同一個倉庫.


而這篇先針對 User and organization Pages sites 說明.

## 如何在 GitHub 上架設 User Pages sites?
1. 要有個認證過的 GitHub account.
2. 建立一個新的倉庫, 重點是倉庫的名稱, `yourAccountName.github.io`, `yourAccountName` 換成你的帳號名.
3. (假設你的開發環境已經有 git) 透過 `git clone` 將剛剛建好的倉庫拉到你的本地開發網頁根目錄. 先將路徑改到你的開發網頁根目錄, 然後執行 `git clone https://github.com/yourAccountName/yourAccountName.github.io.git`.
4. 將你的網頁檔案上傳, 執行以下指令:

        git add -A
        git commit -m "輸入說明"
        git push origin master

這樣就完成了.
