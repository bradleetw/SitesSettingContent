---
title: "Command line 的小技巧 (1)"
date: 2018-08-04T13:51:38+08:00
draft: true
tags: ["command-line", "script"]
categories: ["Useful-Usage"]
featured_image: "/images/yourimagebackgroundfilename.jpg"
description: ""
author: "Brad Lee"
---
## 如何快速將一段文字存入一個檔案?
透過 `>` 或 `>>` 這兩個 output **redirection operators**, 可以快速創建一個檔案或者將一段文字附加在現有檔案後面.

1. **`>` output redirection operator** :

        $ echo "hello world" > filename.tex

    創建一個新檔案並將字串寫入檔案中, 若有相同檔名檔案則覆蓋.

2. **`>>` output redirection operator** :

        $ echo "another sentence append to demo.txt" >> filename.txt

    有相同檔名檔案則將字串直接附加在檔案最後面, 若沒有則直接創練新檔案.

參考博客: [Bash One-Liners Explained, Part I: Working with files](http://www.catonmat.net/blog/bash-one-liners-explained-part-one/)

### 背景知識 -- 關於 I/O redirection operator
https://robots.thoughtbot.com/input-output-redirection-in-the-shell

http://www.catonmat.net/blog/bash-one-liners-explained-part-three/

https://www.cnblogs.com/liuchaogege/p/6124669.html , 從這篇的介紹可以了解一些基本概念.

對電腦而言, 一個共通的運作流程會像是, 收到`輸入`(鍵盤, 滑鼠, 或是時間), 解讀指令然後運算執行, 將結果`輸出`(螢幕, 檔案, 或是網路(socket)).

而 shell command program 被執行起來後, 一直在等待使用者輸入, 在預設的情況下, 標準`輸入`的裝置是鍵盤, 標準`輸出`的裝置是螢幕.

所以當使用者開始透過鍵盤敲下指令和參數, 在還沒有按下 `enter` 鍵前, 每輸入一個字母就會預設在螢幕出現一個字母, 而當按下 `enter` 鍵時 shell command program 就會先確認所輸入的指令和參數(這就是 Parser 的動作)是否合乎格式, 若不正確則將相關的錯誤訊息傳到輸出 - 螢幕, 若正確則開始執行任何指令, 等待執行結束, 將該指令所回傳的訊息傳到輸出 - 螢幕.

而當你想要將原本輸出到螢幕上的結果改存到檔案, 那就要告訴 shell command program 要將預設的輸出裝置(螢幕)改成特定的輸出裝置(檔案), 這時 I/O redirection operator 就派上用場.

例子:

    $ echo "hello world" > demo.tex

echo 這指令是將所跟的參數直接將其傳到 standard output, 在沒有 redirection operator 接在指令後頭時, shell command program 的預設 standard output 就是螢幕, 加上 ` > demo.txt`, 就是表示 standard output 變成 demo.txt 這個檔案.


file decriptor:
0: stdin
1: stdout
2: stderr
