---
title: 用户指南
---

# 用户指南

## 身份认证

在模型管理服务需要验证用户身份时，模型管理命令行工具（以下简称 mmc）有以下两种解决方式。

### 使用用户名和密码

运行 mmc 时添加 `-u <user>` 参数来提供用户名，mmc 会提示用户输入密码，并通过用户名和密码进行身份认证。

!!! note "注意"
    当设置了 `-u <user>` 参数时，mmc 不会从身份配置文件获取用户信息；反之，mmc 只会从身份配置文件获取用户信息，不会提示用户输入用户名或密码。

### 使用身份配置文件

mmc 使用和 Docker 相同格式的身份配置文件，配置文件的路径通过命令行参数 `-c, --config` 进行指定。在未被指定时，使用的默认路径为 `$HOME/.t9k/mmc-config.json`。一个示例如下：

``` bash
{
    "auths": {
        "<host1>": {
            "auth": "dXNlcjpwYXNzd29yZA=="
        },
        "<host2>": {
            "auth": "dXNlcjpwYXNzd29yZA=="
        }
    }
}
```

`mmc login <Host>` 命令可以用来生成、更新身份配置文件，其中的 Host 参数代表模型管理服务的域名。当指定的身份配置文件不存在时，该命令会创建对应的文件，并将身份认证信息保存到这个文件中。当指定的身份配置文件已经存在时，该命令则会更新那个文件。一个身份配置文件中可以保存多个不同 Host，但是每个 Host 中只能保存一个身份。当您用其他身份登录同一个 Host 时，原本的身份信息会被覆盖。

### 特殊情况

在目前模型管理服务器的设置下，用户无法知道一个他没有权限查看的项目是否存在。为了避免泄漏权限外的信息，当您向一个不存在的项目进行上传、下载操作时，也会得到 `401 Unauthorized` 的错误信息。

``` bash
# 向一个不存在的项目上传 modelpack 时
$ mmc push example.com/project_not_exsit/modelpack:1.0.0 modelpack
"Error: unexpected response: 401 Unauthorized"

# 从一个不存在的项目下载 modelpack 时
$ mmc pull example.com/project_not_exsit/modelpack:1.0.0
"Error: unexpected status code [manifests 1.0.0]: 401 Unauthorized"
```

因此，得到 `401 Unauthorized` 的错误信息时，可能是当前用户没有对应操作的权限，也可能是对应的项目不存在。
