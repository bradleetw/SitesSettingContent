---
title: "[GitHub]如何在同一台 mac 中建立兩個不同的 GitHub account ?"
date: 2018-12-18T10:01:29+08:00
draft: false
tags:
    ["Git", "GitHub", "SSH"]
categories:
    ["Tools"]
authors: ["bradlee"]
toc: true
---
# Why need 2 or more Git(Hub) accounts in the same mac?
我現在的目的就只是為了能熟悉 Git 操作, 利用多個 Git accounts 來觀察實驗結果, 而遠端的服務選擇的是 GitHub.

在設定多個帳戶過程中遇到了一些困難, 藉由此篇記錄相關知識.

網路上很多使用者是利用多個 Git accounts 來使得開發者的環境, 可以同時存在個人以及公司的 Source Version Control, 這才是真正的使用場景.

# 2 Major Domain knowledge need to understand
`SSH` and `Git Configuration` 是兩個基礎知識, 本篇記錄這兩個部分.

## SSH (Secure SHell protocol)
目前利用這種密鑰的登入服務是主流方法(因為設定成功後, 使用者就可以不用 type 密碼.), 利用開發者產生的私鑰和公開密鑰, 將公開密鑰放到遠端服務上, 來做匹配帳號的事.

現在我的 mac 上是用 OpenSSH 這個實作 SSH 的 Open Source, 應該是 macOS 的標準配備.


### ssh-keygen
利用 `ssh-keygen` 除了可以產生公鑰和私鑰之外, 呈現密鑰, 還可以管理 `/.ssh/known_hosts` - 一個記錄著你透過 ssh 方式登入過遠端服務器的列表檔案.

#### Generate Key - `ssh-keygen`
底下是常用的生成密鑰命令, 執行成功後會在你設定的路徑(跟在 `-f` 之後)產生私鑰和公鑰(副檔名為 `.pub` )兩個檔案:
```
ssh-keygen -t rsa -b 4096 -C "Developer Key Note" -f ~/.ssh/brad_github_id_rsa
```
`-t`: ssh-keygen support 4 types -- `dsa`, `ecdsa`, `ed25519`,and `rsa`. The default value is `rsa` type(SSH-2).
```
ssh-keygen -t dsa
```
`-f`: Use `-f` to give the file name of private key, and public key with `.pub`. If have no `-f` parameter, `.ssh/id_rsa` or `.ssh/id_dsa` will be the default file name of private key, `.ssh/id_rsa.pub` or `.ssh/id_dsa.pub` will for public key.

`-b`: The length of key. For rsa type key, 最小要求768位，默认是2048位。DSA密钥必须恰好是1024位(FIPS 186-2 标准的要求). In the GitHub online doc, they used 4096.

`-C`: This parameter just is a comment for display, 其實很多講到使用 ssh-keygen 都說 `-C`用 email, 其實不用, 這只是個用來呈現該密鑰是誰或是可以做什麼, 不寫也沒關係, `Provides a new comment` 是 BSD General Commands Manual 對這參數的說明. 若在建立的過程沒加入, 可以後來再透過 `-c` 來添加.

#### Display public key on stdout by inputing private key
```
ssh-keygen -y
ssh-keygen -y -f privateKeyPath
```
可以利用 `-y` 後面接著私鑰的檔名, 結果會輸出公鑰到螢幕.

其實使用者可以直接 `cat` 公鑰的也可以看到.

#### Manage .ssh/known_hosts
當第一次透過 ssh 登入遠端服務器時, 本地端會在 `~/.ssh/known_hosts` 中存放這些遠端服務器的公鑰. 而 `ssh-keygen` 也提供一些方式來管理查看這些遠端服務器的公鑰. 其實使用者可以直接打開 `known_hosts` 觀察.

##### Clear public key in .ssh/known_hosts
```
ssh-keygen -R HostName
```

##### Find specific hostname from .ssh/known_hosts
```
ssh-keygen -F HostName
ssh-keygen -F HostName -l
```

### ssh-agent, ssh-add
http://www.zsythink.net/archives/2407

#### What is the ssh-agent
`ssh-agent` 一個幫助管理私鑰的代理程式, 通常是被預設啟動的, 若沒有被啟動, 用如下的命令呼叫:
```
eval 'ssh-agent'
```
而管理哪些私鑰是透過 `ssh-add` 來加入.

#### ssh-add
```
ssh-add ~/.ssh/id_rsa_personal
```
將特定私鑰加入 `ssh-agent` 這個服務.

#### List all of private key from agent
```
ssh-add -l -E md5
```

#### Move out specific private key from ssh_agent
```
ssh-add -d '~/.ssh/id_rsa_custom'
```

#### Move out all of private key from ssh_agent
```
ssh-add -D
```

## Git Configuration
在 `~/.gitconfig` 中記錄著 git 的 global configuration, 包含了預設編輯器, diff tool, ...等等.

### 設定使用者
```
git config --global user.name "User Name"
git config --global user.email "UserName@email.address"
```
如果你的電腦環境對不同的遠端服務器(或者公司服務器)所記錄的帳號資料都相同, 可以設定成全域值.

這兩個欄位主要是會在 commit log 中顯示的名字和郵件.

不過一般來說對公司的環境, 應該是會用公司的郵件資料. 所以建議這兩個欄位是放在 locale, 也就是根據不同的倉庫對應到個別的 user name/ e-mail. 若要同時可以存在對同一個遠端服務器的多個帳號, 也建議用 locale user name/ email.

在個別的倉庫目錄下設定各自的 user name/ email:
```
git config --local user.name "User Name"
git config --local user.email "UserName@email.address"
```
`--local` 其實可以省略.

### Git clone new repository
如果環境設定中將 `user.name` and `user.emial` 從 global 設定中移除, 那麼在每一次 `git clone git@github.com:someone/some.git` 完之後, 會比較麻煩要額外設定 user.name and user.email locally.

所以只要在 `.zshrc` 中添入如下 alias, 之後只要執行 `gitclone git@github.com:someone/some.git`, 就會一起設定 user.name and user.email.
```
alias gitclone='git clone --config user.name="your name" --config user.email="youremail@address.com" $@'
```

### .ssh/config, 設定遠端服務器資料
打開 `.ssh/config` 可以看到如下的資料:
```
Host github.com-personal
    HostName ssh.github.com
    Port 443
    UseKeychain no
    User git
    IdentityFile ~/.ssh/sgithub_id_rsa
    IdentitiesOnly yes
```
這個檔案裡可以放入多個遠端服務器的資料, 而在 Host 後頭跟著的名稱, 就是當你要決定連到哪一個遠端服務器時, 要填入的名.
```
git clone git@github.com-personal:someone/some.git
ssh -T github.com-personal
```
如果要連到同一個遠端服務器, 但是是用不同的帳號時, 要在 `.ssh/config` 裡在設定一組 Host, 重要的是在新的 Host setting `IdentityFile` 要設成另一個帳號的私鑰檔案.

### Verify whether is workable
```
ssh -T AliasNameInSSH_Config
ssh -vT AliasNameInSSH_Config
```
AliasNameInSSH_Config: 就是在 `.ssh/config` 中每一組遠端服務器設定的 `Host` 欄位, 跟在後面的名字.

相關設定若是正確, 會有以下的顯示輸出:
```
Hi accountNameOfRemoteServer! You've successfully authenticated, but GitHub does not provide shell access.
```
若想知道連接過程的細項流程, 加入 `-vT`.

若失敗就會出現 `Permission denied (publickey).`.

原則上若是單一帳戶的使用場景, 這些設定其實就可以了.

# How to enable second git account in the same mac
1. 利用 `ssh-keygen` 建立另一組新的密鑰.
2. 將新的公鑰上傳至遠端服務器.
3. 利用 `ssh-add` 將新的私鑰放到 `ssh-agent`.
4. 在 `~/.ssh/config` 中增加新的 Host 資料, 並透過 `IdentityFile` 告知所使用的密鑰.
5. 透過 `ssh -T HostName` 檢驗是否設定成功.

設定成功後, 表示你可以用不同帳號下載或 clone, 但不一定可以上傳, 原因就是遠端服務器是否有開上傳權限給你.

## Push failed
原先因為我對 GitHub 的一知半解, 以為所有在 GitHub 上的資料, 除了可以任意下載, 還可以任意上傳. 這樣的觀點只對一半, 若是下載上傳的倉庫都是你自己的單一帳號, 那是沒問題的. 但若是別人的帳號, 上傳的權限就要原倉庫擁有者開放給你, 之後才可以上傳. 就是因為不清楚, 以為前面提的五個步驟設定完成就可以用不同帳號下載上傳, 然後就一直出現以下的 error message.
```
ERROR: Permission to userA/Scripts.git denied to UserB.
fatal: 无法读取远程仓库。

请确认您有正确的访问权限并且仓库存在。
```
GitHub Help reference:
https://help.github.com/articles/error-permission-to-user-repo-denied-to-user-other-repo/

## Set an organization repository
參考以下 GitHub Help 設定合作開發專案:

https://help.github.com/articles/adding-outside-collaborators-to-repositories-in-your-organization/

設定成功後, 在透過 invite other user 來將第二個帳號加入同一個開發專案. 第二個帳號只要接受了邀請, 就可以 push commit.

# Reference
https://blog.alantsai.net/posts/2015/09/use-ssh-in-windows-for-github

https://kuanyui.github.io/2016/08/01/git-multiple-ssh-key/

http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html

https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/
