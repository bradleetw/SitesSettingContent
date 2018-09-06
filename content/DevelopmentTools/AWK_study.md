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
toc: true
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

AWK 可用來對很多有相同格式的文字檔案進行修改, 更新, 或是統計某些文字內容. 而且其 script 的語法借鑒了 C, 所以較容易上手.
很多人在談 AWK 時也都提到 sed, 就初步的了解, sed 是針對 stream text 做處理, 功能比 AWK 弱些, 但我猜是這兩個定位的不同. 之後會再花個時間紀錄一下 sed 的使用方法.

在人工智能及大數據的需求影響下, 很多語言也都提供能讀取固定格式像 csv 的文字檔案, 來進行統計, 然後畫出漂亮有重點的圖, 有這樣的需求 AWK 就較不適用, 因為 AWK 的強項並不在繪圖, 雖然他也可以, 但會比較單調. 而且沒有像 package management 的功能, 導致一些很多高手完成的有用好用的功能無法容易導入.

所以用 AWK 的時機, 就偏向私人大量文檔的修改或統計時來採用.

## 安裝
一般 linux-based 系統都有 AWK 的身影, 理論上不用額外安裝, 像我的 macOS 就內附了. 還有另一個 GAWK, 提供的功能較多, 這個是要額外下載, 但還沒試.

## 如何執行 awk script file
有以下幾種方式:

1. `$ awk '{print $0}' filename.txt`:

    中間`''`放的就是 awk script, 後面就是接著文字檔案, 後面還可以接著更多的檔名, 後面的檔名數量其上限要再花時間深入暸解.

2. `$ awk -f scriptfile.awk filename.txt`:

    將 awk script 寫到檔案中, 其檔名不用加上 `.awk`, 那只是為了個人方便管理. 使用的時候在 awk script file 前面加上 `-f`.

3. 將 awk script file 直接變成可執行的檔案:

    a. 在 awk script file 中的首行加入 `#! /usr/bin/awk -f`.

    b. 變更權限, `$ chmod +x awk_script_file`.

4. `$ ls -al | awk '{ if(substr($1, 1, 1) == "d") print $NF " is direcory." }'`:

    透過 pipeline operator 將前面命令的成功輸出當作輸入.

## 如何編寫 awk script
除了前面提到的 awk script 語法是借鑑 C, 剩下的概念也不難理解.

### 區塊
awk 根據 3 類區塊來決定執行順序, 開始(被執行次數: 1 次) -> 中間(被執行次數: 根據傳入文字檔案的行數決定 ) -> 結束(被執行次數: 1 次):

- **開始區塊**: `BEGIN { statement }`

    承如 `BEGIN` 的含義, 表示這個區塊(區塊的意思是在大括號中間的所有動作)會最先被執行. 主要目的是用來更改一些預設的設定, 如: FS (輸入行的欄位分割符號), RS (輸入行的換行分割符號)...等等, 以及讀取命令行的參數.

	可以多個區塊前面定義為 `BEGIN`, 也可以沒有. awk 會依序先執行所有的 `BEGIN` 區塊, 但只會被執行一次. 但不建議 script 寫成有多個 `BEGIN` 區塊, 一個就好, 這樣語意比較易懂.

- **中間區塊**: `pattern { action }`

    當執行完 `BEGIN` 區塊後, 接著就是依序執行所有的中間區塊, 所有中間區塊被執行的次數是依據被讀取文字輸入檔有多少行來決定. 一般都是在這區塊做資料的判斷統計. 一個 script 中可以沒有中間區塊, 也可以多個.

	可以在 pattern 中加入一些判斷式 ( 判斷式不一定要有, 沒寫就表示 true ), 來決定要不要執行 action.

- **結束區塊**: `END { statement }`

    這個區塊會最後被執行, 而且也只被執行一次, 通常用來輸出統計完的結果(存到檔案, 或是傳到標準輸出), 當然你也可以在中間的區塊做輸出的動作.

	和 `BEGIN` 區塊一樣你可以定義多個 `END` 區塊, 但不建議這樣操作, 每個 script 一個 `END` 區塊就好. 同樣 script 中也可以沒有 `END` 區塊.

---
其實一個 awk script 是由一個或多個的 `pattern { action }` 組合而成, `BEGIN` 和 `END` 只是比較特別.

### 讀取資料
讀取輸入資料: awk 自動讀取所傳入的文字檔案內容或是經由標準輸入傳入的內容, 這是我認爲 awk 好用的地方, 自動讀取資料, 並且將每個欄位自動分開.

#### NF
當在命令列執行 awk script 後頭接上檔名, awk 會自行開檔, 並依序讀取每行資料, 每讀取*一行*, awk 就當作是一筆 Record , 接著執行 script 中的每一個中間區塊, 並將讀到的該筆 Record 中的每個欄位依序放在 `$1`, `$2`, `$3`, ...這些欄位裡, 而 `$NF` 是表示最後一個欄位 (`NF` 紀錄著該行欄位的數量).

#### FNR V.S. NR
`FNR` 則記錄著 awk script 已經讀取當前文字檔案的 Record 次數, 其實想成 `中間區塊` 被執行的次數.

因為 awk script 可以依序處理多個文字檔案, 所以當讀到下一個文字檔案時 `FNR` 又歸零重頭開始紀錄, 而 `NR` 則是將前面已經讀取不同文字檔案的 Record 數量累加起來.

所以我們可以利用這個變數, 來顯示行號.

    { print FNR, $0 }

#### RS
awk 預設是每一行就是一筆 Record, 但也可以改設成多行是一筆 Record. 如下:

	BEGIN { RS = "" }

利用 `RS` 這個變數紀錄著讀取輸入資料時如何判斷是一筆 Record , `"/n"` 是預設的判斷符號, 也就是一行就一筆 Record. 改成 RS = ""(空字串), 會使得 Record 之間是由一個或多個空行來分隔.

#### FS
 而 `" "` (空白符號) 是 awk 在讀取輸入資料時的預設欄位分割符號, 用 `FS` 變數記錄著. 假設你的輸入資料文檔是利用 `,` 來當分割符號, e.g. csv files, 只要有如下設定:

	BEGIN { FS = "," }

讀取 csv 的資料就非常方便. 一般變更 `RS`, `FS` 都是放在 BEGIN 區塊來執行.

#### $0
而 `$0` 記錄著目前讀到的這筆 Record .

#### FILENAME
`FILENAME` 則是用來記錄當前文字檔案名字的變數.

---
### 資料的判斷統計:
當 awk 對輸入資料依序讀取每筆 Record 時, 我們可以依據該 Record 中是否符合某種條件來決定做相對應的動作, 如統計.

#### 篩選 Record
可以在每個 `中間區塊` , `pattern { action }`, 的 `pattern` 的欄位填入判斷式.

##### 沒有 pattern
當 `pattern` 沒有填, 則表示 True, 也就是該 `action` 一定執行.

##### 特定欄位的判斷
可以依據某個欄位是否大於等於小於一特定大小: `<`, `<=`, `==`, `!=`, `>`, `>=`

    $2 > 10 { print $1, $3 * $4 }

第二個欄位要大於 10 才會處理該筆 Record.

    $5 == "January" { print $0 }

只列印 Record 中第五個欄位是 January.

    $2 + $3 > 20 { print $1 }

第二和第三欄位的合要超過 20 才會列印第一個欄位. awk 提供: `&&`, `||`, `!()`

    $2 > 5 && $2 < 20 { print }

第二欄位要在 20 和 5 這個區間才會列印該筆 Record.

#### 變數
##### 自定義變數
變數不需要事先聲明就可以馬上使用. 預設 awk 會給該變數設為 0.

    $3 > 15 { empCounter = empCounter + 1 }
    END     { print empCounter, "employees worked more than 15 hours."}

##### 內建變數
變數 | 意義 | 預設值
---|---|---
ARGC | 命令行参数的个数 | -
ARGV | 命令行参数数组 | -
FILENAME | 当前输入文件名 | -
FNR | 当前输入文件的记录个数 | -
FS | 控制着输入行的欄位分割符 | " "
NF | 当前记录的欄位个数 | -
NR | 到目前为止读的记录数量 | -
OFMT | 数值的输出格式 | "%.6g"
OFS | 输出欄位分割符 | " "
ORS | 输出的记录的分割符 | "\n"
RLENGTH | 被函数 match 匹配的字符串的长度 | -
RS | 控制着输入行的记录分割符 | "\n"
RSTART | 被函数 match 匹配的字符串的开始 |
SUBSEP | 下标分割符 | "\034"

##### 算術運算
awk 提供: `+`, `-`, `*`, `/`, `%`, `^`. 也提供 `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `^=`. 以及 `++`, `--`.

##### 內建算式函數
函數 | 返回值
---|---
atan2(y,x) | y/x 的反正切值, 弧度制, 定义域从 −π 到 π
cos(x) | x 的余弦值, x 以弧度为单位
exp(x) | x 的指数函数, e<sup>x</sup>
int(x) | x 的整数部分; 当 x 大于 0 时, 向 0 取整
log(x) | x 的自然对数 (以 e 为底)
rand() | 返回一个伪随机数r ( 0 <= r < 1 )
sin(x) | x 的正弦值, x 以弧度为单位.
sqrt(x) | x 的方根
srand(x) | 设置随机数种子, 如果省略 x, 则默认使用当天的时间

#### 統計的模式
當所有的 Record 都掃過一遍時, 所需要的資料都已記錄下來, 接著就在 `END { action }` 的 action 做後續的計算輸出動作.

#### 流程控制語句
和 C 的語法類似, 提供: If-Else, While, For, Do-While 等

##### if else
    if (expression)
        statements
    else
        statements

##### while
    while (expression)
        statements

##### do while
    do
        statements
    while (expression)

##### for (初始設定; 條件判斷; 增值)
    for(i = 0; i < 10; i++)
        print $i

##### for (variable in array)
透過此法所得到的 variable 是 array 的 `key`.

    for (i in array)
        print i, array[i]

##### continue v.s. break
continue 和 break 是控制或中斷 while, for, do 這類迴圈的命令.

break 是馬上離開最內層, 不再執行迴圈.

continue 是直接進入下一次的迴圈動作.

##### next v.s. exit
next 與 exit 是控制或中斷讀取輸入資料的命令.

next 使 awk 抓取下一個 Record, 然後從第一個 `中間區塊`繼續.

在 `END 區塊` 中執行 `exit` 會導致程序終止, 而在其他的區塊裡, `exit` 會使得程序表現得好像所有的輸入資料都讀完了, 不會再有輸入資料被讀取, 接著就直接執行 `END 區塊`

#### 字串處理

##### 字串相加

    { names = names $1 " " }
    END { print names }

##### 內建字串函數
函數 | 描述
---|---
gsub(r,s)   | 将 $0 中所有出现的 r 替换为 s, 返回替换发生的次数.
gsub(r,s,t )    | 将字符串 t 中所有出现的 r 替换为 s, 返回替换发生的次数
index(s,t)  | 返回字符串 t 在 s 中第一次出现的位置, 如果 t 没有出现 的话, 返回 0.
length(s)   | 返回 s 包含的字符个数
match(s,r)  | 测试 s 是否包含能被 r 匹配的子串, 返回子串的起始位置 或 0; 设置 RSTART 与 RLENGTH
split(s,a)  | 用 FS 将 s 分割到数组 a 中, 返回欄位的个数
split(s,a,fs)   | 用 fs 分割 s 到数组 a 中, 返回欄位的个数
sprintf(fmt,expr-list)  | 根据格式字符串 fmt 返回格式化后的 expr-list
sub(r,s)    | 将 $0 的最左最长的, 能被 r 匹配的子字符串替换为 s, 返 回替换发生的次数.
sub(r,s,t)  | 把 t 的最左最长的, 能被 r 匹配的子字符串替换为 s, 返回 替换发生的次数.
substr(s,p) | 返回 s 中从位置 p 开始的后缀.
substr(s,p,n)   | 返回 s 中从位置 p 开始的, 长度为 n 的子字符串.

---
### 輸出結果
利用 `print` 和 `printf` 這兩個命令將所要的資料結果輸出, `printf` 的格式和 C 是類似的.

#### printf 格式
fmt | $1 | printf(fmt, $1)
---|---|---
%c, ASCII 字符 | 97 | a
%d, 10 進制整數 | 97.5 | 97
%5d | 97.5 | ___97 (`_` 表示空白)
%e, 科學記號表示 | 97.5 | 9.750000e+01
%f, 浮點數 | 97.5 | 97.500000
%7.2f | 97.5 | __97.50 (`_` 表示空白)
%g, 按照 %e or %f 進行轉換, 選擇較短的那個, 無意義的零會被抑制| 97.5 | 97.5
%.6g | 97.5 | 97.5
%o, 無符號 8 進制 | 97 | 141
%06o | 97 | 000141
%x, 無符號 16 進制 | 97 | 61
%s, 字符串 | January | January
%10s | January | ___January (`_` 表示空白)
%-10s | January | January___ (`_` 表示空白)
%.3s | January | Jan
%10.3s | January | _______Jan (`_` 表示空白)
%-10.3s | January | Jan_______ (`_` 表示空白)
%%, 打印一个百分号 %, 不会有参数被吸收 | | %


#### 輸出到螢幕
將結果打印到標準輸出, 也就是螢幕:

	{ print $2, $NF }
    { printf("The 2nd field is %d, %.2f", $2, $2*$4) }

#### 存到檔案
將結果輸出到檔案: 透過 redirector command `>` (將輸出結果存到檔案, 會將原有資料覆蓋) or `>>` (將輸出結果附加到檔案).

    { printf("$1=%d, $2=%d", $1, $2) > "outFileName.txt" }


**PS**:`{ print $1, $2 > $3 }` 和 `{ print $1, ($2 > $3) }` 的差別:

第一個式子是將 $1 和 $2 的輸出結果存到一個以 $3 內容來命名的檔案, 第二個式子是將 $1 以及 $2 是否大於 $3 的結果輸出到螢幕.

#### 傳到下個命令
將結果透過 pipeline operator, `|` , 傳給 下一個命令: 目前我所看到的用法都是將輸出結果傳到 `sort` 這命令將結果做排序.

    BEGIN   { FS = "\t" }
            { pop[$4] += $3 }
    END     { for (c in pop)
                printf("%15s\t%6d\n", c, pop[c]) | "sort -t'\t' +1rn"
            }

其實也可以在命令列底下來執行相同的事:

	$ awk -f someScript.awk data.txt | sort -t'\t' +1rn

#### OFS, ORS
這兩個變數是在使用 `print expression, expression, ...` 命令時用到的. 打印各個 expression, expression 之間由 OFS 分開, 由 ORS 終止.

`OFS` 預設的輸出欄位分割符號是`" "`, 而`ORS` 預設的輸出換行符號是`"\n"`.

`{ print $1, $2, $3 }` 輸出結果:

    Beth 4.00 0
    Dan 3.75 0
    Kathy 4.00 10

`{ print $1 $2 $3 }` 輸出結果: (這語法是將$1,$2,和$3變成一個字串)

    Beth4.000
    Dan3.750
    Kathy4.0010

加上 `BEGIN{ OFS = "-"}` 其 `{ print $1, $2, $3 }`輸出結果變成:

    Beth-4.00-0
    Dan-3.75-0
    Kathy-4.00-10



- [GNU AWK 官方使用手冊.](http://www.gnu.org/software/gawk/manual/gawk.html#toc-Getting-Started-with-awk)

- [簡單的介紹 sed & awk & grep 入門.](https://www.cnblogs.com/moveofgod/p/3540575.html)

- [用一些例子介紹 sed & awk.](http://dongweiming.github.io/sed_and_awk/#/)

- [Github 上一本介紹 awk programming 的中文翻譯.](https://github.com/wuzhouhui/awk)
