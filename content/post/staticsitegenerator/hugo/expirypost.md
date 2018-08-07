---
title: "[Hugo]如何讓帖子一定時間後自動關閉"
date: 2018-08-07T11:20:48+08:00
draft: true
tags: ["static-site-generator", "hugo"]
categories: ["Web"]
featured_image: "/images/time-273857_1920.jpg"
description: ""
author: "Brad Lee"
---
## 讓帖子自動關閉
當作者貼出新的文章只希望在一段時間內給讀者閱讀, 只要依照本文的操作, 就能在時間到期後自動徹帖.

## 為何要啟動倒數自動徹帖
有時因為文章內容敏感, 或是故作神秘, 還有可能是為了飢餓行銷, 當然也有可能只是為了管理過多的文章, 所以才啟動定時徹帖. 只要設定將 `expiryDate` 欄位給定特定日期, 時間到就能自動關閉該文章.

## 添加 expiryDate 欄位
只要在每一篇 Markdown 檔案開頭的 frontmatter 區段加入 `expiryDate`, 如下:

    ---
    title: "The Example Doc"
    date: 2018-08-07
    expiryDate: 2018-09-07
    ---

當然本帖是不會自動關閉的.
