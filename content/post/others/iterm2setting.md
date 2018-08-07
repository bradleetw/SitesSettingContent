---
title: "讓 iTerm2 有很酷炫的外表!"
date: 2018-07-29T17:41:05+08:00
draft: false
description: ""
tags: ["iTerm2", "zsh"]
categories: ["Useful-Usage"]
featured_image: "/images/iTerm2withGoodTheme.png"
---
常看到電影裡的駭客在操作電腦時所用的 command line 都是那麼的酷, 今天就來速記一下參考網路上別人分享設定的步驟. 參考的來源: [超簡單！十分鐘打造漂亮又好用的 zsh command line 環境](https://medium.com/statementdog-engineering/prettify-your-zsh-command-line-prompt-3ca2acc967f)


iTerm2 的安裝就沒記錄, 因為早就安裝過, 安裝流程也不難.

## 安裝 [zsh](http://www.zsh.org/) + [oh-my-zsh](http://ohmyz.sh)
`zsh` 是類似 `bash`, 在一般的使用上兩者差不多, 而 `zsh` 要再搭配上 `oh-my-zsh`(它是基於 `zsh` 的一個擴展工具集, 提供了豐富的擴展功能), 就可以設置有趣的主題風格(Themes), 而 `oh-my-zsh` 本身就提供了很多主題可以讓你挑選.

1. **安裝 zsh**:

        $ brew install zsh

2. **將 zsh 改成預設 shell**:

        $ sudo sh -c "echo $(which zsh) >> /etc/shells"
        $ chsh -s $(which zsh)

3. **安裝 oh-my-zsh**:

        $ wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh
        $ bash ./install.sh

## 安裝 zsh theme: [powerlevel9k](https://github.com/bhilburn/powerlevel9k)

1. **下載好用的主題**:

    一些高手都推薦 `powerlevel9k` 這個主題, 它利用很多的特殊符號呈現很多的訊息, 方便使用者閱讀.  `powerlevel9k` 並不是 `oh-my-zsh` 預設提供的主題, 需要另外下載.

        $ git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k

2. **變更主題**:

    打開 `.zshrc`, 將 `ZSH_THEME` 改成 `"powerlevel9k/powerlevel9k"`. 並且加上如下兩行資料:

        POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir dir_writable vcs vi_mode)
        POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status background_jobs ram load time)

    接著請執行 `exec $SHELL`. 漂亮的主題就出現了.

    powerlevel9k 的相關功能請參閱  [The most awesome Powerline theme for ZSH around!](https://github.com/bhilburn/powerlevel9k#available-prompt-segments).

## 安裝 Nerd fonts
裝完新的 `oh-my-zsh` 主題風格 - powerlevel9k, 可能會發現一些亂碼, 原因是這每一個亂碼就代表了一特殊功能的狀態, 需要特殊的圖示來呈現, 但目前的字型並未支持, 所以我們要來安裝特殊的字型.

1. **安裝字型**:

    我們要選擇 [Nerd-fonts](https://github.com/ryanoasis/nerd-fonts) 這一系列的字型, 該系列的字型有較全的符號, 而且更新頻繁.

    因為是透過 `brew` 來安裝字型, 所以必須先執行,

        $ brew tap caskroom/fonts

    接著搜索 `Nerd-fonts`, 可以找到很多.

        $ brew search nerd

    我就直接使用高手的推薦, 選用 `font-sourcecodepro-nerd-font`.

        $ brew cask install font-sourcecodepro-nerd-font

2. **iTerm2 變更字型**:

    從 `Preference -> Profiles -> Text -> Change Font` 挑選剛剛安裝好的字型. 新版的 `iTerm2` 可以讓 ASCII 和 Non-ASCII 兩類文字設定成不同的字型, 我們這裡先不用這麼花俏, 都用相同的字型即可.


## 如何讓 iTerm2 呈現漂亮顏色的字?
1. **設定 Report Terminal Type**:

    將 `Preference -> Profiles -> Terminal -> Report Terminal Type` 改成 `xterm-256color`.

2. **設定賞心悅目的顏色組**:

    從 `Preference -> Profiles -> Colors -> Color Presets...` 挑選一組自認不錯顏色組. iTerm2 本身有附帶幾組, 我原本也就使用這些內附的, 但還不夠好看. 所以要從網路上去下載高手們提供的顏色組, GitHub 就有 [iTerm2-Color-Schemes](https://github.com/mbadolato/iTerm2-Color-Schemes), 請先自行下載下來, 再透過 `Preference -> Profiles -> Colors -> Color Presets... -> import...` 將下載資料匯入(在下載的目錄 `schemes` folder 底下有很多的 itermcolors files) , 我直接依照高手所推薦, 挑選 `Tomorrow Night Eighties.itermcolors` 這個顏色組. 因為匯入完成並不會直接套用這個顏色組, 所以請再選擇這個顏色組 `Preference -> Profiles -> Colors -> Color Presets... -> Tomorrow Night Eighties`.

以上這些安裝設定步驟完成後, 你的 command line 呈現效果就會像以下的樣子.

![調整完畢的示意圖](/images/iTerm2withGoodTheme.png)
