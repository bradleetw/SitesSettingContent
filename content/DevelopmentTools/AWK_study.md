---
title: "AWK_Study"
date: 2018-08-19T16:24:52+08:00
draft: true
tags:
    - awk
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
## AWK
AWK 是一種程式語言, 針對有固定格式的文字檔案或是命令列執行結果進行處理, 可統計, 然後依據其結果來做顯示, 或將結果存入檔案, 或傳輸到"標準輸出".

## 為什麼用 AWK
若是要對很多有相同格式的文字檔案進行修改, 更新, 或是統計某些文字內容, 可用 AWK. 而且其 script 的語法借鑒了 C, 所以較容易上手.
很多人在談 AWK 時也都提到 sed, 就初步的了解, sed 是針對 stream text 做處理, 功能比 AWK 弱些, 但我猜是這兩個定位的不同. 之後會再花個時間紀錄一下 sed 的使用方法.

在人工智能及大數據的需求影響下, 很多語言也都提供能讀取固定格式的像 csv 的文字檔案, 進行統計, 然後畫出漂亮有重點的圖, 這樣的需求 AWK 就較不適用, 雖然他也可以, 但沒有像 package management 的功能, 導致一些很多高手完成的有用好用的功能無法容易導入.

所以用 AWK 的時機, 就偏向私人大量文檔的修改或統計時來採用.

## 安裝
一般 linux-based 系統都有 AWK 的身影, 理論上不用額外安裝, 像我的 macOS 就內附了. 還有另一個 GAWK, 提供的功能較多, 這個是要額外下載, 但我還沒試.

## 如何執行 awk script file
1. `$ awk '{print $0}' filename.txt`

    中間`''`放的就是 awk script, 後面就是接著文字檔案, 後面還可以接著更多的檔名, 後面的檔名數量其上限要再花時間深入暸解.[to do item ]

2. `$ awk -f scriptfile.awk filename.txt`

    將 awk script 寫到檔案中, 其檔名不用加上 `.awk`, 那只是為了個人方便管理. 使用的時候在 awk script file 前面加上 `-f`.

3. 將 awk script file 直接變成可執行的檔案

    awk scipt file 也可以變成命令, 其步驟:

    - 在 awk script file 中的首行加入 `#! /usr/bin/awk -f`.
    - 加入可執行的權限, `$ chmod +x awk_script_file`.

4. `$ ls -al | awk '{ if(substr($1, 1, 1) == "d") print $NF " is direcory." }'`

    透過 pipeline operator 將前面命令的成功輸出當作輸入.

## 如何編寫 awk script
除了前面提到的 awk script 語法是借鑑 C, 剩下的概念也不難理解.

1. 主要分成 3 區塊:

    - 開始區塊:
        `BEGIN { action }`

    - 中間區塊:
        `pattern { action }`

        - pattern:

        - action:
        
    - 結束區塊:
        `END { action }`

- [GNU AWK 官方使用手冊.](http://www.gnu.org/software/gawk/manual/gawk.html#toc-Getting-Started-with-awk)

- [簡單的介紹 sed & awk & grep 入門.](https://www.cnblogs.com/moveofgod/p/3540575.html)

- [用一些例子介紹 sed & awk.](http://dongweiming.github.io/sed_and_awk/#/)

- [Github 上一本介紹 awk programming 的中文翻譯.](https://github.com/wuzhouhui/awk)
