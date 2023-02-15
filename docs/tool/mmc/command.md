---
title: 命令
---

# 命令

## 帮助信息

您可以使用 `--help` 参数查看命令行工具的帮助信息。

``` bash
# 查看命令行工具的帮助信息
mmc --help

# 查看 login 命令的帮助信息
mmc login --help
```

## 初始化 Modelpack

模型管理服务要求模型遵守 [Modelpack 格式规范](../../module/model/modelpack.md)。`init` 命令可以帮助生成其中的 `metadata.yaml` 文件。

``` bash
mkdir -p ./mnist/model
mmc init ./mnist
```

这样产生的 `mnist` 文件夹可以被模型管理服务识别并使用（尽管其中没有任何有用的信息）。您可以将模型相关的文件分别存放在 `mnist` 文件夹下的 `code`、`datasets`、`docs`、`model`、`metrics` 文件夹中，并修改 `metadata.yaml` 文件的值。这样您就会得到一个可以通过模型管理服务来使用的模型。

## 登录

运行 `login` 命令登录到模型管理服务器。您可以根据命令行提示来输入用户名和密码，或者通过命令行参数 `-u` 指定用户名，`-p` 指定密码。

``` bash
export HOST=mms.tsz.io
mmc login $HOST
```

<figure>
  <img alt="login" src="../../assets/tool/mmc/mmc_login.gif"/>
</figure>

登录后的身份认证信息保存在配置文件中，命令行参数 `-c, --config`。详见[使用身份配置文件](user-guide.md#使用身份配置文件)。

## 查看模型

运行 `inspect` 命令查看指定模型的元数据（metadata）。

``` bash
mmc inspect $HOST/t9kpublic/mnist:1.0.0
```

<figure>
  <img alt="inspect" src="../../assets/tool/mmc/mmc_inspect.gif"/>
</figure>

## 下载模型

运行 `pull` 命令下载模型。

``` bash
mmc pull $HOST/t9kpublic/mnist:1.0.0 ./mnist
```

!!! hint "提示"
    在模型管理控制台可以复制下载指令。

<figure>
  <img alt="pull" src="../../assets/tool/mmc/mmc_pull.gif"/>
</figure>

## 上传模型

运行 `push` 命令上传模型。

``` bash
mmc push $HOST/t9kpublic/mnist:1.0.0 ./mnist
```
<figure>
  <img alt="push" src="../../assets/tool/mmc/mmc_push.gif"/>
</figure>
