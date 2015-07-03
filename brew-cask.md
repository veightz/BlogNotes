title: brew cask - 让生活更美好
date: 2014-08-30 00:29:23
categories: 
- TECH
- Homebrew
tags: [homebrew, brew, cask]
---
# 前言
------
homebrew 是Mac下一个包管理工具， 可以方便得安装Mac下许多命令行工具。
而cask是brew的增强工具，提供了更丰富的GUI应用程序。
# 安装Homebrew
------
## 在终端输入命令
```
ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```
## 如果遇到需要安装Command Line Tools
<!-- more -->
```
xcode-select --install
```

# 安装cask
------
## 在终端输入命令
```
brew tap phinze/cask
brew install brew-cask
```

## 使用brew cask
---
### 比如我现在想要安装 wireshark 

```
brew cask search wireshark
```
输入结果：
```
==> Exact match
wireshark
```
那我就放心的输入：
```
brew cask install wireshark
```
就行了。

### 查看brew cask的软件库
```
brew cask search
```
你会发现数量实在是。。。。多。别说是QQ了， 连qq音乐都有.

### 删除
```
brew cask remove <target_name>
```

> 其实就是比单纯用brew时，后边都加了个 cask . =_=!
