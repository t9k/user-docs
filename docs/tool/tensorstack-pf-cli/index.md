---
title: TensorStack PortForward CLI
---

# TensorStack PortForward CLI

TensorStack PortForward CLI（简称 t9k-pf) 是 TensorStack AI 平台的命令行工具，其功能类似于 `kubectl port-forward`，使用户能够在本地通过端口转发的方式访问 TensorStack AI 平台的各种资源。目前支持的资源类型有 Notebook、Pod、Service。

## 准备

### 安装

t9k-pf 可以从平台首页下载。请根据操作系统和架构（可以在命令行运行 `uname -om` 获取）选择适当的版本，并根据下载的版本，设置 t9k-pf 的版本和系统架构等变量：

``` bash
version=0.1.9
os=darwin
arch=amd64
```

然后解压下载好的 t9k-pf，并把得到的二进制文件移动到 `/usr/local/bin` 路径下：

``` bash
tar -zxvf "$HOME/Downloads/t9k-pf-$version-$os-$arch.tar.gz"
mv t9k-pf-$os-$arch /usr/local/bin/t9k-pf
rm -f "$HOME/Downloads/t9k-pf-$version-$os-$arch.tar.gz"
```

安装完成后，运行以下命令来验证安装是否成功：

``` bash
t9k-pf -h
```

如果要卸载 t9k-pf，直接删除对应位置的二进制文件即可。

### 身份认证和授权

t9k-pf 会默认使用 `$HOME/.t9k/t9k-config.yaml` 路径下 T9k Config 中 current-context 的认证信息进行身份认证。您可以通过命令行参数 `-c, --config` 来指定 t9k-pf 使用的 T9k Config 文件的路径。

下面是一个 T9k Config 的示例，其中 current-context 为 `demo1`，`demo1` 对应 context 下的 auth 的 token 不为空，因此最终 t9k-pf 使用该值 `demo1-token` 来完成身份验证（如果 apikey 和 token 均不为空，t9k-pf 优先使用 apikey）。

``` yaml
current-context: demo1
contexts:
- name: demo1
  server: https://<example.com>
  image-registry: https://<example.io>
  prefixes:
    aimd: /t9k/aimd/server
    asset-hub: /t9k/asset-hub/server
    build-console: /t9k/build-console/server
    cluster-admin: /t9k/cluster-admin/server
    deploy-console: /t9k/deploy-console/server
    workflow: /t9k/workflow/server
  auth:
    apikey: ""
    token: demo1-token
  extension:
    codepack:
      data-copy-image: <your-image>
- name: demo2
  server: https://<example.com>
  ...
```

!!! note "注意" 
    如果默认的 T9k Config 文件不存在，您可以先了解 [T9k Config](../tensorstack-cli/user-guide.md#配置文件) 相关内容，并生成默认文件。

如果默认配置文件不符合您的要求，您可以编辑您使用的 T9k Config 文件。或者临时通过命令行参数 `-k,--apikey` 直接指定 API Key。例如输入以下指令（其中 `notebook <URL>` 相关命令会在下文介绍，此处只用关注 `--apikey` 的使用）：

``` bash
t9k-pf notebook <URL> --apikey
```

命令行会进入交互式输入界面，粘贴您的 API Key 再按下回车即可。

## 使用手册

### 访问 Pod

您可以通过 t9k-pf 命令行工具访问指定 Pod 的指定端口。其主要用法如下：

首先请确定要连接的 Pod 的名称（name）以及命名空间 （namespace）。下文中我们会用 `<Name>` 代表 Pod 的名称，`<Namespace>` 代表 Pod 的命名空间。

然后请确定要连接的目标端口以及本地进行端口转发的端口（如果不指定，会随机指定本地监听的端口）。下文中我们会用 `<LocalPort>` 代表本地监听的端口，`<TargetPort>` 代表目标 Pod 的端口。

!!! note "注意"  
    小于 1024 的端口需要管理员权限才可以绑定。

最后请确认您使用的 TensorStack port-forward 服务端的地址。该地址一般为您所使用的 TensorStack AI 平台的域名加上 `/t9k/port-forward`，如果不能确定地址，请咨询管理员。确认地址后，需要通过 `-t` 来指定该值,下文中我们会用 `<Host>` 来代表服务端的地址。

确定了以上信息后，在命令行中输入以下命令，便可开启端口转发：

``` bash
t9k-pf pod <Name> <LocalPort>:<TargetPort> -n <Namespace> -t <Host>
```

!!! note "注意"  
    此处的 namespace 不和 t9kctl 和 kubectl 共享，如果您不通过 -n 指定 namespace，该值会被设为'default'。

例如输入：

``` bash
t9k-pf pod example 3333:2222 -n dev
```

命令行会打印出 `127.0.0.1:3333`， 然后您便可通过本地的该端口访问到命名空间 dev 下的 Pod example 的 2222 端口。

您也可以不指定本地端口，例如输入 ：

``` bash
t9k-pf pod example 2222 -n dev
```

命令行会随机返回一个本地端口，例如 `127.0.0.1:57873`。然后您便可通过本地的该端口访问到命名空间 dev 下的 Pod example 的 2222 端口。

!!! note "注意" 
    在 port-forward 成功后，您仍然需要保持您的 t9k-pf 命令行窗口一直保持运行状态。

### 访问 Service

您可以通过 t9k-pf 命令行工具访问指定 Service 的指定端口。其用法与访问 Pod 的方法类似。例如输入：

```
t9k-pf service example 3333:2222 -n dev
```

您便可以在本地通过 3333 端口访问 Service example 的 2222 端口。

### 访问 Notebook

针对 TensorStack AI 平台的 Notebook 资源，我们提供了直接通过其 URL 地址获取 SSH 连接方式的功能。使用该命令，您不再需要指定名称、命名空间以及服务端地址。

其用法如下：

``` bash
t9k-pf notebook <URL> <LocalPort>
```

其中 `<URL>` 代表地址栏中的地址，`<LocalPort>` 代表您指定的本地端口号，如果不指定，会返回随机端口。

!!! note "注意"  
    与前面不同，为了方便用户快速连接 SSH，t9k-pf 命令行不支持指定 Notebook 资源的目标端口。如果您有相关需求，可以先获取 Notebook 对应的 Pod 资源，然后参照[访问 Pod ](#访问-pod)来访问特定的目标端口。

例如输入：

``` bash
t9k-pf notebook <tensorstack-host>/t9k/build-console/projects/demo/notebooks/demo-notebook/lab/tree/demo.ipynb 3333
```

您便可以在本地通过 3333 端口访问 demo 项目下的 demo-notebook 的 SSH 端口。关于 SSH 连接的详细内容请参阅[通过 SSH 连接远程使用 Notebook](../../guide/develop-and-test-model/use-notebook-remotely-via-ssh-connection.md)。

## Flags 参考

* **-c, --config**

    T9k Config 文件的路径。

* **-k, --apikey**

    开启交互式输入 API Key。

* **-n, --namespace** 

    目标资源的命名空间。

* **-t, --t9kServiceHost**

    TensorStack port-forward 服务端的地址，该地址一般为您所使用的 TensorStack AI 平台的域名加上 `/t9k/port-forward`，如果您不能确定该地址，请咨询管理员。
