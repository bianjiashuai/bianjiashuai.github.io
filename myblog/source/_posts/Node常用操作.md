---
title: Node常用工具
date: 2019-11-15 14:13:25
tags:
cover: img/node/node-cover.jpg
---

## Node版本管理工具 nvm

### 1、安装nvm

* 如果已经单独安装了node，建议卸载。
* 直接进入安装包下载地址：[https://github.com/coreybutler/nvm-windows/releases](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fcoreybutler%2Fnvm-windows%2Freleases)，选择nvm-setup.zip，下载后直接安装。 
* 使用命令`nvm -v`检查是否安装成功

### 2、安装Node

使用`nvm install <version> [<arch>]`命令下载需要的版本。arch参数表示系统位数，默认是64位，如果是32位操作系统，需要执行命令：nvm install 8.11.2 32

### 3、Node版本管理

* `nvm nvm list` 是查找本电脑上所有的node版本
  * `nvm list` 查看已经安装的版本
  *  `nvm list installed` 查看已经安装的版本
  *  `nvm list available` 查看网络可以安装的版本

* `nvm install` 安装最新版本nvm

* `nvm use <version>` 切换使用指定的版本node

* `nvm ls` 列出所有版本

* `nvm current` 显示当前版本

* `nvm alias <name> <version>`  给不同的版本号添加别名

* `nvm unalias <name>` 删除已定义的别名

* `nvm reinstall-packages <version>` 在当前版本node环境下，重新全局安装指定版本号的npm包

* `nvm on` 打开nodejs控制

* `nvm off` 关闭nodejs控制

* `nvm proxy` 查看设置与代理

* `nvm *_mirror [url]` 设置

  * `nvm node_mirror [url]` 设置或者查看setting.txt中的node_mirror，

    如果不设置的默认是 https://nodejs.org/dist/

  * `nvm npm_mirror [url]` 设置或者查看setting.txt中的npm_mirror，

    如果不设置的话默认的是： https://github.com/npm/npm/archive/.

* `nvm uninstall <version>` 卸载指定的版本

* `nvm use [version] [arch]` 切换指定的node版本和位数

* `nvm root [path]` 设置和查看root路径

* `nvm version` 查看当前的版本

## Node镜像管理工具

### 1、安装nrm

使用命令`npm install -g nrm`安装nrm

### 2、Node镜像管理

* `nrm ls`  列出所有镜像，如下：

  ```shell
    npm -------- https://registry.npmjs.org/
    yarn ------- https://registry.yarnpkg.com/
    cnpm ------- http://r.cnpmjs.org/
  * taobao ----- https://registry.npm.taobao.org/
    nj --------- https://registry.nodejitsu.com/
    npmMirror -- https://skimdb.npmjs.com/registry/
    edunpm ----- http://registry.enpmjs.org/
  ```

* `nrm use <name>` name 表示镜像名称，如：nrm use taobao

* `nrm add name url `添加自定义的npm源，name 为自定义源名称 ，url为npm源链接