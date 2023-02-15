---
title: 安装
---

# 安装

## 下载

模型管理命令行工具（以下简称 mmc）可以从平台首页下载。您需要根据操作系统和架构（可以在命令行运行 `uname -om` 获取）选择适当的版本。

## 安装

您需要根据下载的版本，设置 mmc 的版本和系统架构等变量：

``` bash
version=1.41.0
os=darwin
arch=amd64
```

然后解压下载好的 mmc，并把它移动到 `/usr/local/bin` 路径下：

``` bash
tar -zxvf "$HOME/Downloads/mmc-$version-$os-$arch.tar.gz"
mv mmc-$os-$arch /usr/local/bin/mmc
rm -f "$HOME/Downloads/mmc-$version-$os-$arch.tar.gz"
```

您可以运行以下命令来验证 mmc 安装完成：

``` bash
mmc version
```
## 卸载

删除二进制文件以卸载 mmc：

``` bash
rm -f /usr/local/bin/mmc
```
