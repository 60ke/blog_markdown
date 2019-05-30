---
title: homebrew的安装与卸载
date: 2018-12-13 14:04:54
categories: Mac
tags: []
urlname: 107
---
# brew的安装
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# brew的卸载
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"

## homebrew cask的安装
    brew tap phinze/homebrew-cask
    brew install brew-cask

## homebrew cask的卸载
`brew install brew-cask`

## 可视化homebrew安装工具

`brew cask install cakebrew`
## 图形化管理Homebrew安装的服务软件

`brew tap jimbojsb/launchrocket`
`brew cask install launchrocket`


## 终端工具

`brew cask install iterm2`
`//配色https://github.com/mbadolato/iTerm2-Color-Schemes`

## shadowsocks客户端

`brew cask install shadowsocksx-ng`

## perl升级
`sudo perl -MCPAN -e 'CPAN::Shell->notest(install => CPAN::Shell->r)'`






