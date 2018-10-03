---
title: "[Python] virtualenv, virtualenvwrapper, pyenv, and pipenv"
date: 2018-09-18T12:17:10+08:00
draft: false
tags:
    ["virtualenv", "virtualenvwrapper", "autoenv", "pyenv", "pipenv"]
categories:
    - Python
authors: ["bradlee"]
toc: true
---
## Python 為什麼需要虛擬開發環境
開發者的電腦中也許同時存在多個開發項目但需要同一個 package 的不同版本, 所以需要利用像是 virtualenv 這類的工具來建立不同的獨立開發環境.

## 利用 virtualenv 建立虛擬開發環境
首先利用 `pip` 安裝: `$ pip install virtualenv`.

### 建立虛擬環境
先為你要開發的項目建立一個目錄, 然後進入該附錄後, 執行以下命令來建立虛擬開發環境.
```
$ virtualenv --no-site-packages VenvName
```
如果想要建立的虛擬環境也要有和當前系統一樣的第三方包, 更換參數
```
$ virtualenv --system-site_packages VenvName
```

### 進入虛擬環境
成功後, `$ source VenvName/bin/activate` 進入該虛擬開發環境.

可利用 `$ pip list` 查看目前環境所安裝的第三方包. 接著就可以安裝所需要的第三方包.

### 離開虛擬環境
`$ deactivate` 就可離開該虛擬開發環境.

## 利用 virtualenvwrapper 管理所有的虛擬環境
單純使用 `virtualenv` 來進行開發是沒什麼大問題, 但在面臨同時在一台電腦中有多個開發項目, 使用 virtualenvwrapper 可以幫忙管理 (建立, 選擇使用, 移除 虛擬空間)多個虛擬空間. 而且提供更方便進入開發虛擬空間的命令.

### 安裝 virtualenvwrapper
安裝 `$ pip install virtualenvwrapper`.

### 啟動 virtualenvwrapper
`$ source /usr/local/bin/virtualenvwrapper.sh`

若要常使用 `virtualenvwrapper`, 將上面命令加入 `~/.zshrc` or `~/.bashrc` 中. 并添上以下內容:
```
export VIRTUALENV_USE_DISTRIBUTE=1        #  总是使用 pip/distribute
export WORKON_HOME=$HOME/.virtualenvs        # 所有虚拟环境存储的目录
if [ -e $HOME/.local/bin/virtualenvwrapper.sh ];then
    source $HOME/.local/bin/virtualenvwrapper.sh
else if [ -e /usr/local/bin/virtualenvwrapper.sh ];then
          source /usr/local/bin/virtualenvwrapper.sh
     fi
fi
export PIP_VIRTUALENV_BASE=$WORKON_HOME
export PIP_RESPECT_VIRTUALENV=true
```
`virtualenvwrapper` 將各項目所建立的`虛擬`目錄集中到 `~/.virtualenvs` (預設值), 使用 `workon VenvName` 就可直接進入各個項目的虛擬開發環境, 並且進入該目錄.

### 相關命令
- `$ mkvirtualenv -p python3.6 env36`: 建立虛擬空間

- `$ mkvirtualenv VenvName`: 建立虛擬空間

- `$ workon VenvName`: 進入虛擬空間

- `$ deactivate`: 離開虛擬空間

- `$ workon` 列出所有透過 virtualenvwrapper 安裝的虛擬環境

- `$ rmvirtualenv VenvName`: 移除虛擬空間

## autoenv
這提供讓使用者利用 `cd` 進入某目錄時, 可以自動執行你所設定的特定命令. 只要在你想要有作用的目錄下建立 `.env` 的文字檔, 內容寫下想要執行的命令.

https://github.com/kennethreitz/autoenv

### 安裝
```
$ brew install autoenv
$ echo "source $(brew --prefix autoenv)/activate.sh" >> ~/.zshrc
```

### autoenv 結合 virtualenv or virtualenvwrapper
利用 autoenv 可以讓你進入開發目錄時, 直接就啟動虛擬空間. 在 `.env` 這個檔案中寫入 `workon VenvName` or `source VenvName/bin/activate`.

## pyenv
除了利用 vituralenv 來設定虛擬開發環境, 還可以用 `pyenv` 來讓不同的目錄有不同的 python 版本. 但要注意, pyenv 只能管理透過由 pyenv 安裝的 python.

### 安裝
`$ brew install pyenv`

在 `.zshrc` 裡加入以下環境變數:
```
export PATH="/Users/bradlee/.pyenv:$PATH"
eval "$(pyenv init -)"
```
### 相關命令
`$ pyenv versions` : 查看目前已安裝的 python

`$ pyenv install --list` : 查看可以安裝的 python

`$ pyenv install 2.7.4` : 安裝特定版本 python

`$ pyenv global 2.7.4` : 設定全域 (整台電腦) 環境所使用的 python version

`$ pyenv local 2.7.4` : 設定當前目錄環境所使用的 python version

`$ pyenv local --unset` : 移除當前目錄環境所設定的 python version.

`$ pyenv uninstall 2.7.4` : 移除特定版本的 python

## 如何記錄 Python 開發時所需要的 Library
利用 virtualenv + virtualenvwrapper 這兩個套件讓我們建立以及管理虛擬開發環境, 但是環境中的第三方 Pakcage 還是要自己管理.

利用 pip + requirements.txt 來記錄開發時所需要的 Python Library, 以便在另一個環境時可以很快利用 requirements.txt 來重裝 Python Libary.

利用 `$ pip install packageName` 安裝, 再利用 `$ pip freeze > requirements.txt` 紀錄所需要的 packages 以及其相關版本.

`$ pip install -r requirements.txt`, 依據 requirements.txt 的描述來安裝 packages.

因為 requirements.txt 中並不會紀錄 package 彼此的依存關係, 所以要直接利用修改 requriements.txt 將不要的 packages 移除, 會有誤刪 (有可能別的 package 也用到你所刪的) 的可能性.

而在 pip 的官方文件中描述 https://pip.pypa.io/en/stable/reference/pip_uninstall/ 有兩類被安裝的 packages 是無法透過 `pip uninstall` 被移除.

## pipenv
pipenv is a packages dependency management of python.
[參考1](http://www.dongwm.com/archives/使用pipenv管理你的项目/),
[pipenv source code](https://github.com/pypa/pipenv),
[pipenv 官方網站](https://pipenv.readthedocs.io/en/latest/)

前面描述了利用 virtualenv, pip 來建立虛擬環境及 package management, 而 pipenv 可以同時達成這兩個目的.

**主要特性包含**：

1. 根据 Pipfile 自动寻找项目根目录。
2. 如果不存在，可以自动生成 Pipfile 和 Pipfile.lock。
3. 自动在项目目录的 .venv 目录创建虚拟环境。（当然这个目录地址通过设置WORKON_HOME改变）
4. 自动管理 Pipfile 新安装和删除的包。
5. 自动更新 pip。

**Pipfile的基本理念是**：

1. Pipfile 文件是 TOML 格式而不是 requirements.txt 这样的纯文本。
2. 一个项目对应一个 Pipfile，支持开发环境与正式环境区分。默认提供 default 和 development 区分。
3. 提供版本锁支持，存为 Pipfile.lock。

### 安裝
`$ brew install pipenv`

### 基本相關命令
`$ pipenv --three`: 建立一個以 python 3 的虛擬環境, 以及 Pipfile.

`$ pipenv --two`: 建立 python 2 的虛擬環境, 以及 Pipfile.

`$ pipenv install`: 若該目錄中未建立過虛擬環境, 則先建立 python 3 的虛擬環境和 Pipfile, 然後同時產生 Pipfile.lock. 若該目錄底下有 Pipfile & Pipfile.lock 則會依據內容安裝.

`$ pipenv install packagename1 packagename2`: 安裝 package. 同時會在 Pipfile 中紀錄所安裝的 package name.

`$ pipenv install packgaeName==1.1`: 安裝特定版本的 package

`$ pipenv install devUsePackageName --dev`: 所安裝的 package 只用於開發測試環境.

`$ pipenv install -d`: 若該目錄中未建立過虛擬環境, 則先建立 python 3 的虛擬環境和 Pipfile, 然後同時產生 Pipfile.lock. 若該目錄底下有 Pipfile & Pipfile.lock 則會依據內容安裝開發測試環境用的 package.

`$ pipenv install -r path/to/requirements.txt`: 依據之前開發時所用的 requirements.txt 來安裝 packages.

`$ pipenv shell`: 進入虛擬開發環境.

`$ pipenv graph`: Pipenv 觀察所安裝的 package 關係.

`$ pipenv --rm`: 刪除虛擬環境.

`$ pipenv uninstall packageName`: 刪除安裝的第三方 package.

`$ pipenv run python xxx.py`: 利用該虛擬環境來執行 xxx.py, 可額外設定 `alias prp=’pipenv run python’`, prp xxx.py 就可直接執行

`$ pipenv lock -r`: 產生 requirements.txt.

`$ pipenv update --outdated`: Find out what’s changed upstream.

`$ pipenv update`: Want to upgrade everything.

`$ pipenv update <pkg>`: for each outdated package.

### pypi source 改成牆內
有時安裝 package 的時間會很長, 有兩種說法: pypi source 在牆外, Pipfile.lock 的寫檔時間過長.

方法一: 可以直接更改 pipfile 的 source url:

```
[[source]]
 url = "https://pypi.tuna.tsinghua.edu.cn/simple"
 verify_ssl = true
 name = "pypi"
```

方法二: 設定環境變數 **PIPENV_PYPI_MIRROR**

方法三: 透過安裝命令 `$ pipenv install --pypi-mirror <mirror_url>`

```
$ pipenv install --pypi-mirror <mirror_url>
$ pipenv update --pypi-mirror <mirror_url>
$ pipenv sync --pypi-mirror <mirror_url>
$ pipenv lock --pypi-mirror <mirror_url>
$ pipenv uninstall --pypi-mirror <mirror_url>
```

### 進階用法
為不同的 package 指定不同的 source
```
[[source]]
url = "https://mirrors.aliyun.com/pypi/simple"
verify_ssl = true
name = "aliyun"

[[source]]
url = "https://pypi.douban/simple"
verify_ssl = true
name = "douban"

[dev-packages]

[packages]
requests = {version="*", index="douban"}
maya = {version="*", index="aliyun"}
records = "*"
```

### 目前遇到 pipenv 的問題
1. 安裝 package 時間過久, 似乎是在處理 Pipfile.lock 時消耗太多時間 (目前我還沒有成功安裝一個 package), 開發者已經在處理此問題. 目前解決方法, `pipenv install packageName --skip-lock`, 省略 pipfile.lock 的步驟.

2. 在預設建立開發環境時,  pipenv 會使用 python 3.7, 而目前 tensorflow 還無法相容於 python 3.7, https://github.com/pypa/pipenv/issues/2619.

## Reference

[Python environment with Pipenv, Jupyter, and EIN](https://matthewbilyeu.com/blog/python-environment-with-pipenv-jupyter-and-ein/)

[使用pipenv管理你的项目](http://www.dongwm.com/archives/使用pipenv管理你的项目/),

[pipenv source code](https://github.com/pypa/pipenv),

[pipenv 官方網站](https://pipenv.readthedocs.io/en/latest/)
