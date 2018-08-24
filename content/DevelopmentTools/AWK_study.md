---
title: "AWK_Study"
date: 2018-08-19T16:24:52+08:00
draft: true
tags:
categories:
cover:
    image: /images/yourimagebackgroundfilename.png
    caption:
    style: wide
authors: ["bradlee"]
slug:
toc: false
comments: false
emoji: false
flowchart: false
viz: false
mathjax: false
msc: false
wave: false
---
## AWK ——是什么？目的是什么？做什么工作？
AWK 是一種程式語言, 主要針對文字檔案處理或者是 Shell script 處理:
1. 文字檔案處理: 將一個或多個文檔當作輸入, 根據你要找尋的文字, 執行你要的動作, 例如: 替代, 統計, 然後再將結果傳到 Standard Output ('$1') 或者檔案.
    例子: 讀取 csv file, 統計相關欄位資料, 產生妳想要的資料.
2. Shell script處理: 透過 Standard Input ('&0'), 或者經由 Pipeline 接收前一個命令執行完傳到 Standard Output ('&1') 當作輸入資料, 執行你要的動作, 然後再將結果傳到 Standard Output ('$1') 或者檔案.
    例子: '$> ll | awk '{ if(substr($1, 1, 1) == "-") print $9 " is a file." }' ' 將 ll 命令的結果傳到 awk program, 讀取資料完後, 只打印出檔案的名稱.

## WHY——为什么？为什么要这么做？理由何在？原因是什么？

## WHERE——何处？在哪里做？从哪里入手？

## WHO——谁？由谁来承担？谁来完成？谁负责？

## WHEN——何时？什么时间完成？什么时机最适宜？

## HOW——怎么做？如何提高效率？如何实施？方法怎样？

## HOW MUCH——多少？做到什么程度？数量如何？质量水平如何？费用产出如何？

- [GNU AWK 官方使用手冊.](http://www.gnu.org/software/gawk/manual/gawk.html#toc-Getting-Started-with-awk)

- [簡單的介紹 sed & awk & grep 入門.](https://www.cnblogs.com/moveofgod/p/3540575.html)

- [用一些例子介紹 sed & awk.](http://dongweiming.github.io/sed_and_awk/#/)

- [Github 上一本介紹 awk programming 的中文翻譯.](https://github.com/wuzhouhui/awk)
