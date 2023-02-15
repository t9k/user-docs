---
title: Dataset Management CLI
---

# Dataset Management CLI

本文档介绍[数据集管理](../../module/dataset)模块中命令行工具的使用方法，包括 `lakectl` 和 `s3cmd`。其中， `s3cmd` 主要用于上传、下载文件，`lakectl` 主要用于版本控制和权限管理相关的操作。另外，`lakectl` 的使用方法也可以参阅 [lakeFS 官方文档:octicons-link-external-16:](https://docs.lakefs.io/reference/commands.html){target=_blank}。

## 准备工作

### 下载

`lakectl` 可以从平台首页下载。您需要根据操作系统和架构选择适当的版本，下载后将其解压并移动到 `/usr/local/bin` 路径下：

```bash
version=v0.63.0
os=darwin
arch=amd64

tar -zxvf ./lakectl-$version-$os-$arch.tar.gz
mv ./lakectl-$os-$arch /usr/local/bin/lakectl
rm ./lakectl-$version-$os-$arch.tar.gz
```

您可以运行以下命令来验证 `lakectl` 安装完成：

```bash
lakectl --version
```

`s3cmd` 可以通过以下命令安装：

```bash
# Ubuntu
sudo apt-get install s3cmd

# macOS
brew install s3cmd
```

您可以运行以下命令来验证 `s3cmd` 安装完成：

```bash
s3cmd --version
```

另外，[Notebook](../../module/building/notebook.md) 中已经预装了 `lakectl` 和 `s3cmd`，您无需手动安装。

### 配置

`lakectl` 和 `s3cmd` 都通过配置文件来进行配置，它们的配置文件分别位于 `$HOME/.lakectl.yaml` 和 `$HOME/.s3cfg`。

假设您在 lakeFS 中的账号密码分别为 `USERNAME` 和 `PASSWORD`，lakeFS 的地址为 `http://example.com`，那么配置文件的形式如下：

??? quote "`$HOME/.lakectl.yaml`"
    ```yaml
    credentials:
      access_key_id: USERNAME
      secret_access_key: PASSWORD
    server:
      endpoint_url: http://example.com/api/v1
    ```

??? quote "`$HOME/.s3cfg`"
    ```bash
    # Setup endpoint
    host_base = http://example.com
    host_bucket = http://example.com
    bucket_location = us-east-1
    use_https = False

    # Setup access keys
    access_key = USERNAME
    secret_key = PASSWORD

    # Enable S3 v4 signature APIs
    signature_v2 = False
    ```

## 使用手册

下面具体介绍数据集管理过程中 `lakectl` 和 `s3cmd` 的使用方法。

### repo 操作

#### 创建 repo

创建 repo 时需要在底层的 S3 存储服务中指定一个路径来存放该 repo 中的数据。我们已经提前创建好了一个名为 t9k 的 bucket，如果您要创建一个名为 myrepo 的 repo，指定路径为 `s3://t9k/myrepo` 即可。

```bash
lakectl repo create lakefs://myrepo s3://t9k/myrepo
lakectl repo create lakefs://another-repo s3://t9k/another-repo
```

#### 列出所有的 repo

```bash
lakectl repo list
```

#### 删除 repo

```bash
lakectl repo delete lakefs://another-repo
```


### branch 操作

#### 新建 branch

```bash
# 基于 main branch 新建一个 branch
lakectl branch create lakefs://myrepo/mybranch \
  --source lakefs://myrepo/main
# 基于一个 commit 新建一个 branch
lakectl branch create lakefs://myrepo/mybranch \
  --source lakefs://myrepo/50440c4ab941b1c7a8497741f
```

#### 列出所有 branch

```bash
lakectl branch list lakefs://myrepo
```

#### 合并 branch

在没有冲突的情况下，您可以将一个 branch 合并到另一个 branch 中。

```bash
lakectl merge lakefs://myrepo/source-branch \
  lakefs://myrepo/destination-branch
```

#### 删除 branch

```bash
lakectl branch delete lakefs://myrepo/mybranch
```

#### 受保护的 branch

如果一个 branch 是受保护的，那么只允许别的 branch 被合并到这个 branch 上，而不允许对这个 branch 做任何直接的修改。

```bash
# 将 myrepo 中的 mybranch 设置为受保护的
lakectl branch-protect add lakefs://myrepo mybranch

# 将 myrepo 中符合 stable-* 格式的 branch 设置为受保护的，例如名为 stable-v1.0、stable-2.3.4 的 branch
lakectl branch-protect add lakefs://myrepo stable-*
```


### 文件操作

#### 本地上传文件

支持上传单个文件、多个文件（使用通配符）和整个目录。

```bash
s3cmd put ./object s3://myrepo/mybranch
s3cmd put ./*.png s3://myrepo/mybranch
s3cmd put -r ./mnist/training/ s3://myrepo/mybranch
```

#### 提交 commit

```bash
lakectl commit lakefs://myrepo/mybranch -m "Add first object"
```

#### 查看 commit 记录

```bash
lakectl log lakefs://myrepo/mybranch
```

#### 查看文件列表

```bash
s3cmd ls s3://myrepo/mybranch/
s3cmd ls s3://myrepo/mybranch/mydirectory/
```

#### 下载文件

支持下载单个文件和整个目录。

```bash
s3cmd get s3://myrepo/mybranch/myobject ./
s3cmd get -r s3://myrepo/mybranch/mydirectory ./
```

#### 删除文件

支持删除单个文件和整个目录。

```bash
s3cmd rm s3://myrepo/mybranch/myobject
s3cmd rm -r s3://myrepo/mybranch/mydirectory
```


### tag 操作

#### 创建 tag

```bash
# 为一个 branch 当前最新的 commit 加上 tag
lakectl tag create lakefs://myrepo/v1 lakefs://myrepo/mybranch
# 为任意一个 commit 加上 tag
lakectl tag create lakefs://myrepo/v2 \
  lakefs://myrepo/5eeb5f7ba39f36d4bad495e
```

#### 列出所有 tag

```bash
lakectl tag list lakefs://myrepo
```

#### 删除 tag

```bash
lakectl tag delete lakefs://myrepo/v0
```


### 用户操作

!!! note "注意"
    这些创建、删除用户、用户组操作需要当前用户属于 [Admins 用户组](#权限操作)。

#### 创建用户

```bash
lakectl auth users create --id your-username
```

#### 生成用户登录信息

```bash
lakectl auth users credentials create --id your-username
```

将生成的 Access Key ID 和 Secret Access Key 保存在 `$HOME/.lakectl.yaml` 中、或者在网页中登录，即可以该用户的身份访问 lakeFS。

#### 列出所有用户

```bash
lakectl auth users list
```

#### 删除用户

```bash
lakectl auth users delete --id your-username
```

### 权限操作

我们通过将用户加入到某个用户组（group）中来设置用户权限。以下是内置的用户组及其所拥有的权限：

* Admins：
    * 读、写所有 repo
    * 创建、删除 repo
    * 创建、删除用户、用户组
* Developers：
    * 读、写所有 repo
* Viewers:
    * 读所有 repo

#### 添加用户权限

```bash
lakectl auth groups members add --user your-username --id group-name
```

例如，设置用户 test-user 能够读、写所有 repo 可使用如下命令：

```bash
lakectl auth groups members add --user test-user --id Developers
```

#### 删除用户权限

```bash
lakectl auth groups members remove --user your-username --id group-name
```

#### 列举用户权限

```bash
lakectl auth users groups list --id your-username
```

#### 列举具有某个权限的用户

```bash
lakectl auth groups members list --id group-name
```
