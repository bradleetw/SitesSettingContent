---
title: "讓 iTerm2 也翻牆"
date: 2019-07-19T23:00:05+08:00
draft: false
description: ""
tags: ["iTerm2", "zsh"]
categories: ["Tools"]
cover:
    image: /images/iTerm2withGoodTheme.png
    style: wide
authors: ["bradlee"]
---

[Reference](<https://github.com/Quinton/blog/issues/2>)

 首先環境必須先安裝好 shadowsocks.

## 安裝 `polipo`

```cmd
brew install polipo
```

## 設定 `polipo`

### `polipo` 開機自啟動

```cmd
atom /usr/local/opt/polipo/homebrew.mxcl.polipo.plist
```

在 `homebrew.mxcl.polipo.plist` 中加上 `socksParentProxy=localhost:1080`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
  <plist version="1.0">
    <dict>
      <key>Label</key>
      <string>homebrew.mxcl.polipo</string>
      <key>RunAtLoad</key>
      <true/>
      <key>KeepAlive</key>
      <true/>
      <key>ProgramArguments</key>
      <array>
        <string>/usr/local/opt/polipo/bin/polipo</string>
        <string>socksParentProxy=localhost:1080</string>
      </array>
    </dict>
  </plist>
```

```cmd
ln -sfv /usr/local/opt/polipo/*.plist ~/Library/LaunchAgents
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.polipo.plist
```

#### 若要從自啟動中取消

```cmd
launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.polipo.plist
```

### 設置別名

在 `.zshrc` 中加入以下命令:

```sh
alias proxy="export http_proxy=http://localhost:8123;export https_proxy=http://localhost:8123"
alias unproxy="unset http_proxy"
```

## 使用

啟動, 當然 SS 必須先啟動

```cmd
proxy
```

關閉

```cmd
unproxy
```