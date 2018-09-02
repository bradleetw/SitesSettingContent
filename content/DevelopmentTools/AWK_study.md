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
1. `$ awk '{print $0}' filename.txt`:

    中間`''`放的就是 awk script, 後面就是接著文字檔案, 後面還可以接著更多的檔名, 後面的檔名數量其上限要再花時間深入暸解.[to do item ]

2. `$ awk -f scriptfile.awk filename.txt`:

    將 awk script 寫到檔案中, 其檔名不用加上 `.awk`, 那只是為了個人方便管理. 使用的時候在 awk script file 前面加上 `-f`.

3. 將 awk script file 直接變成可執行的檔案:

    awk scipt file 也可以變成命令, 其步驟:

    - 在 awk script file 中的首行加入 `#! /usr/bin/awk -f`.
    - 加入可執行的權限, `$ chmod +x awk_script_file`.


4. `$ ls -al | awk '{ if(substr($1, 1, 1) == "d") print $NF " is direcory." }'`:

    透過 pipeline operator 將前面命令的成功輸出當作輸入.

## 如何編寫 awk script
除了前面提到的 awk script 語法是借鑑 C, 剩下的概念也不難理解.

1. awk 根據 3 類區塊來決定執行順序, 開始(被執行次數: 1 次) -> 中間(被執行次數: 根據傳入文字檔案的行數決定 ) -> 結束(被執行次數: 1 次):

    - 開始區塊:
        `BEGIN { statement }`

        承如 `BEGIN` 的含義, 表示這個區塊(區塊的意思是在大括號中間的所有動作)會最先被執行. 主要目的是用來更改一些預設的設定, 如: FS (輸入行的字段分割符號), RS (輸入行的換行分割符號)...等等, 以及讀取命令行的參數. 可以多個區塊前面定義為 `BEGIN`, 也可以沒有. awk 會依序先執行所有的 `BEGIN` 區塊, 但只會被執行一次. 但不建議 script 寫成有多個 `BEGIN` 區塊, 一個就好, 這樣語意比較易懂.

    - 中間區塊:
        `pattern { action }`

        當執行完 `BEGIN` 區塊後, 接著就是依序執行所有的中間區塊, 所有中間區塊被執行的次數是依據被讀取文字輸入檔有多少行來決定. 一般都是在這區塊做資料的判斷統計. 一個 script 中可以沒有中間區塊, 也可以多個. 我們可以在 pattern 中加入一些判斷式 ( 判斷式不一定要有, 沒寫就表示 true ), 來決定要不要執行 action.

    - 結束區塊:
        `END { statement }`

        這個區塊會最後被執行, 而且也只被執行一次, 主要用來輸出統計完的結果(存到檔案, 或是傳到標準輸出), 當然你也可以在中間的區塊做輸出的動作. 和 `BEGIN` 區塊一樣你可以定義多個 `END` 區塊, 但不建議這樣操作, 每個 script 一個 `END` 區塊就好. 同樣 script 中也可以沒有 `END` 區塊.

2. 自動讀取所傳入的文字檔案內容或是經由標準輸入傳入的內容: 這是我認爲 awk 好用的地方, 自動讀取資料, 並且將每個字段自動分開.

    當在命令列執行 script 後頭接上檔名, awk 會自行開檔, 並依序讀取每行資料, 每讀取一行 awk 就會執行每一個中間區塊, 並將每個字段依序放在 $1, $2, $3, ...這些欄位裡.

3. 輸出

4.

- [GNU AWK 官方使用手冊.](http://www.gnu.org/software/gawk/manual/gawk.html#toc-Getting-Started-with-awk)

- [簡單的介紹 sed & awk & grep 入門.](https://www.cnblogs.com/moveofgod/p/3540575.html)

- [用一些例子介紹 sed & awk.](http://dongweiming.github.io/sed_and_awk/#/)

- [Github 上一本介紹 awk programming 的中文翻譯.](https://github.com/wuzhouhui/awk)
