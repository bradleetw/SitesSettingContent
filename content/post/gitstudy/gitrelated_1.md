---
title: "[Git]如何忽略追蹤特定檔案或目錄?"
date: 2018-08-08T11:49:49+08:00
draft: false
tags: ["Git"]
categories: ["Tools"]
featured_image: "/images/gitstudy/devops-3155972_1920.jpg"
description: ""
author: "Brad Lee"
---
只要編輯以下三個檔案(忽略清單)其中一個就可以忽略追蹤特定檔案或目錄:

1. **$HOME/.config/git/ignore**: 開發者電腦中的所有倉庫都可以讀取該忽略清單.
2. **.gitignore**: 每個倉庫都有自己一份的忽略清單放在該倉庫根目錄下, 而且該忽略清單可以被分享追蹤管理.
3. **.git/info/exclude**: 該忽略清單無法被追蹤管理.

### $HOME/.config/git/ignore
有時候系統或者一些第三方應用為了讓其運作的效果更好, 會在目錄底下產生一些額外的檔案, 列如: `.DS_Store`, 而這些對開發者本身而言這類無關開發的資料都是不必要去追蹤紀錄, 這時可以透過編輯 `$HOME/.config/git/ignore` 來寫下要忽略的檔案, 而這個是對系統內的所有倉庫都有用. 以下是該檔案內的一些範例:

    # General
    .DS_Store
    .AppleDouble
    .LSOverride
    # Files that might appear in the root of a volume
    .DocumentRevisions-V100
    .fseventsd
    .Spotlight-V100
    .TemporaryItems
    .Trashes
    .VolumeIcon.icns
    .com.apple.timemachine.donotpresent

### .gitignore
在開發的環境中會因為編譯產生執行檔案, 連結檔, 某些檔案或是某些目錄開發者根本不必追蹤, 但是這個忽略清單卻是可以分享給其他開發者或者需要版本管控忽略清單 (有可能在經過一段的開發時間, 開發環境導入了新的機制或是功能, 而產生新的不必追蹤檔案) 這時只要在開發項目的根目錄下放入 `.gitignore`, 在該檔案中寫入你要忽略上傳的特定檔案或目錄:

1. 特定檔案: 直接放入檔案名稱, ex: `somefolder/specific.txt`

2. 符合特定字串的檔案: 加入萬用字元, ex: `/db/*.sqlite3`

3. 目錄: ex: `somefolder/`

建議: `.gitignore` 這個檔案也可被忽略, 只要將 .gitignore 寫入, 但是不建議忽略.

GitHub 上放了很多範例 https://github.com/github/gitignore.

參考網頁: https://gitbook.tw/chapters/using-git/ignore.html

### .git/info/exclude
若有一些在開發環境下的檔案不需要被追蹤上傳而且這忽略規則清單也不必分享追蹤管理, 列如: 個人的 memo.txt, 則可以在該倉庫底下的 `.git/info/exclude` 檔案中加入忽略規則.
