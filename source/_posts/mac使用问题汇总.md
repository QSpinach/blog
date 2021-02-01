---
tags: [MAC]
comments: true
toc: true
---

# mac使用问题汇总

### 如何安装nginx
安装homebrew，使用brew安装nginx
查看是否安装nginx
```
brew search nginx
```
安装ginx
```
brew install nginx
```
nginx安装路径`/usr/local/etc/nginx/`
启动nginx，默认访问8080端口
```
nginx
```
关闭nginx
```
nginx -s stop
```

### 如何安装homebrew
国内安装
```ssh
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```
官方安装
```
 $ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)" 
```

也可以加速克隆
```
BREW_REPO="https://github.com/Homebrew/brew"
# 变成：
BREW_REPO="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git"
```
其他镜像安装
```
# brew 程序本身，Homebrew/Linuxbrew 相同
git -C "$(brew --repo)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git

# 以下针对 mac OS 系统上的 Homebrew
git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
git -C "$(brew --repo homebrew/cask)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask.git
git -C "$(brew --repo homebrew/cask-fonts)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask-fonts.git
git -C "$(brew --repo homebrew/cask-drivers)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask-drivers.git

# 以下针对 Linux 系统上的 Linuxbrew
git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/linuxbrew-core.git

# 更换后测试工作是否正常
brew update
```

恢复
```
# brew 程序本身，Homebrew/Linuxbrew 相同
git -C "$(brew --repo)" remote set-url origin https://github.com/Homebrew/brew.git

# 以下针对 mac OS 系统上的 Homebrew
git -C "$(brew --repo homebrew/core)" remote set-url origin https://github.com/Homebrew/homebrew-core.git
git -C "$(brew --repo homebrew/cask)" remote set-url origin https://github.com/Homebrew/homebrew-cask.git
git -C "$(brew --repo homebrew/cask-fonts)" remote set-url origin https://github.com/Homebrew/homebrew-cask-fonts.git
git -C "$(brew --repo homebrew/cask-drivers)" remote set-url origin https://github.com/Homebrew/homebrew-cask-drivers.git

# 以下针对 Linux 系统上的 Linuxbrew
git -C "$(brew --repo homebrew/core)" remote set-url origin https://github.com/Homebrew/linuxbrew-core.git

# 更换后测试工作是否正常
brew update
```
### 如何展示隐藏文件及文件夹

```
# 关闭显示隐藏文件的话就把上面的命令中YES改为NO就行了
defaults write com.apple.Finder AppleShowAllFiles YES
killall Finder
```

### 安装 webstorm 2020.3.2
```
# 删除配置信息目录

rm -rf ~/Library/Preferences/WebStorm*

# 删除插件信息目录

rm -rf ~/Library/Application\ Support/WebStorm*

# 缓存信息目录

rm -rf ~/Library/Caches/WebStorm*

# 删除日志信息目录

rm -rf ~/Library/Logs/WebStorm*

# 删除Webstorm.vmoptions
cd /Users/leitianxiao/Library/Application\ Support//JetBrains/Webstorm2020.2/Webstorm.vmoptions

rm -f  Webstorm.vmoptions
```