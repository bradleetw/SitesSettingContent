---
title: "Julia Language"
date: 2018-08-21T16:27:25+08:00
draft: false
tags: [Julia]
categories: [JuliaLang]
authors: ["bradlee"]
---
MIT 开发的 Julia 语言是全球热度上升最快的编程语言之一，下载量超过 200 万次，下载者包括谷歌、Facebook、FAA 和美国能源部等各个部门的开发者。近日，MIT CSAIL 实验室正式发布了 Julia 1.0，该语言期望结合 C 的速度、Matlab 的数学表征、Python 的通用编程与 Shell 的胶水命令行，并构建开源、自由与便捷的编程语言。

## Julia 的特點, 參考[Julia 1.0](https://julialang.org/blog/2018/08/one-point-zero-zh_tw), 節錄其中一段:

- **快速**：Julia 一開始就是為高效能設計的。 Julia 可以藉由 **LLVM** 被編譯成不同平台的高效機器碼。

> LLVM: 可參考[[LLVM每日谈之一 LLVM是什么](https://blog.csdn.net/snsn1984/article/details/8036032)]. 節錄其中一段, "LLVM 的主要作用是它可以作为多种语言的后端，它可以提供可编程语言无关的优化和针对很多种CPU的代码生成功能".

- **泛用**：Julia 使用多重分派（multiple dispatch）作為程式典範（paradigm），可以更容易表達物件導向和函數-式的設計模式。標準函式庫提供了非同步 I/O，行程控制，日誌記錄，效能分析，套件管理器等等。

- **動態**：Julia 是動態型別的，用起來像腳本語言，並且很好地支援互動式的操作方式。

- **技術**：Julia 擅長數值運算，有非常貼近數學的語法，支援多種數值型別，並且支援平行運算。Julia 的多重分派結合數值和陣列相關的資料型別可以說是渾然天成。

- **選擇性的型別標註**：Julia 有豐富的資料型別描述，型別宣告可以使得程式更加清楚和穩固。

- **組合性**：Julia 的套件可以很和諧的一起運作。矩陣的單位數量或是資料表中一行的貨幣和顏色可以一起運作並且擁有良好的效能。

---
這個新的語言能作什麼, 目前還說不上, 只知道這是個從 MIT 出來, 集大家需求而生的一個開源新語言, 不想掉隊, 只有先學再說了.

目前先從 2 個線上的資源開始

1. [Programming in Julia](https://lectures.quantecon.org/jl/index_learning_julia.html)

2. [A Deep Introduction to Julia for Data Science and Scientific Computing](http://ucidatascienceinitiative.github.io/IntroToJulia/)

接下來就依這兩個資源邊學邊寫讀後感.
