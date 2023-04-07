# Notebook 标准镜像列表

由平台提供和维护的 Notebook 镜像称为 Notebook 标准镜像。每个 Notebook 标准镜像提供某一种流行的机器学习框架作为其主要环境，同时预装了一些 Python 包、[命令行工具](#命令行工具)和最新版本的[平台工具](../../tool/index.md)。

当前正在维护的 Notebook 标准镜像如下表所示：

| 名称                                                            | 主要环境     | 备注     |
| --------------------------------------------------------------- | ------------ | -------- |
| [tensorflow-1.15.5-notebook-cpu](#tensorflow-1155-notebook-cpu) | TensorFlow 1 | CPU 镜像 |
| [tensorflow-1.15.5-notebook-gpu](#tensorflow-1155-notebook-gpu) | TensorFlow 1 | GPU 镜像 |
| [tensorflow-2.12.0-notebook-cpu](#tensorflow-2120-notebook-cpu) | TensorFlow 2 | CPU 镜像 |
| [tensorflow-2.12.0-notebook-gpu](#tensorflow-2120-notebook-gpu) | TensorFlow 2 | GPU 镜像 |
| [torch-1.13.1-notebook](#torch-1131-notebook)                   | PyTorch 1    |          |
| [torch-2.0.0-notebook](#torch-200-notebook)                     | PyTorch 2    |          |

这些镜像会持续更新，直到相应机器学习框架的小版本更新后被新镜像替代，此时旧镜像会被放到[不再维护的 Notebook 标准镜像](#不再维护的-notebook-标准镜像)列表中。镜像的标签是它的版本号，其跟随平台的版本号进行更新；镜像的每一次更新可能包含修复问题、更新包或工具、更新 Notebook 的扩展程序等内容。

标签中包含 `-sudo` 的镜像包含 `sudo` 命令，其中用户（`t9kuser`）的密码为 `tensorstack`。

如要自定义 Notebook 镜像，请参阅[构建 Notebook 自定义镜像](./build-notebook-custom-image.md)。

## tensorflow-1.15.5-notebook-cpu

镜像基于 [`tensorflow/tensorflow:1.15.5-jupyter`:octicons-link-external-16:](https://hub.docker.com/layers/tensorflow/tensorflow/1.15.5-jupyter/images/sha256-47aa058918aa7b09343c05ccbd23ccef976006a07b579143e9adde34a937b419?context=explore){target=_blank}（[基础镜像介绍:octicons-link-external-16:](https://hub.docker.com/r/tensorflow/tensorflow){target=_blank}）。

## tensorflow-1.15.5-notebook-gpu

镜像基于 [`tensorflow/tensorflow:1.15.5-gpu-jupyter`:octicons-link-external-16:](https://hub.docker.com/layers/tensorflow/tensorflow/1.15.5-gpu-jupyter/images/sha256-5f2338b5816cd73ea82233e2dd1ee0d8e2ebf539e1e8b5741641c1e082897521?context=explore){target=_blank}（[基础镜像介绍:octicons-link-external-16:](https://hub.docker.com/r/tensorflow/tensorflow){target=_blank}），故包含以下 NVIDIA GPU 库：

| 库      | 版本     |
| ------- | -------- |
| CUDA    | 10.0     |
| cuDNN   | 7.6.2.24 |
| nvinfer | 5.1.5    |

## tensorflow-2.12.0-notebook-cpu

镜像基于 [`tensorflow/tensorflow:2.12.0-jupyter`:octicons-link-external-16:](https://hub.docker.com/layers/tensorflow/tensorflow/2.12.0-jupyter/images/sha256-c70fc19788a8c11dd3d81bbeb492deb72a2d67b1875759366b96ed6821264eca?context=explore){target=_blank}（[基础镜像介绍:octicons-link-external-16:](https://hub.docker.com/r/tensorflow/tensorflow){target=_blank}）。

## tensorflow-2.12.0-notebook-gpu

镜像基于 [`tensorflow/tensorflow:2.12.0-gpu-jupyter`:octicons-link-external-16:](https://hub.docker.com/layers/tensorflow/tensorflow/2.12.0-gpu-jupyter/images/sha256-fffb1d07831e488af8372053342bfe8c77052e34d6e85dbe4a37b10a4f6072b0?context=explore){target=_blank}（[基础镜像介绍:octicons-link-external-16:](https://hub.docker.com/r/tensorflow/tensorflow){target=_blank}），故包含以下 NVIDIA GPU 库：

| 库      | 版本      |
| ------- | --------- |
| CUDA    | 11.8      |
| cuDNN   | 8.6.0.163 |
| nvinfer | 8.4.3     |

## torch-1.13.1-notebook

镜像基于 [`pytorch/pytorch:1.13.1-cuda11.6-cudnn8-devel`:octicons-link-external-16:](https://hub.docker.com/layers/pytorch/pytorch/1.13.1-cuda11.6-cudnn8-devel/images/sha256-58d848c38665fd3ed20bee65918255cb083637c860eb4fae67face2fb2ff5702?context=explore){target=_blank}（[基础镜像介绍:octicons-link-external-16:](https://hub.docker.com/r/pytorch/pytorch){target=_blank}），故包含以下 NVIDIA GPU 库：

| 库    | 版本     |
| ----- | -------- |
| CUDA  | 11.6     |
| cuDNN | 8.4.0.27 |
| NCCL  | 2.12.10  |

## torch-2.0.0-notebook

镜像基于 [`pytorch/pytorch:2.0.0-cuda11.7-cudnn8-devel`:octicons-link-external-16:](https://hub.docker.com/layers/pytorch/pytorch/2.0.0-cuda11.7-cudnn8-devel/images/sha256-96ccb2997a131f2455d70fb78dbb284bafe4529aaf265e344bae932c8b32b2a4?context=explore){target=_blank}（[基础镜像介绍:octicons-link-external-16:](https://hub.docker.com/r/pytorch/pytorch){target=_blank}），故包含以下 NVIDIA GPU 库：

| 库      | 版本     |
| ------- | -------- |
| CUDA    | 11.7     |
| cuDNN   | 8.5.0.96 |
| NCCL    | 2.13.4   |

## 命令行工具

所有镜像包含以下命令行工具：

| 名称   | 介绍                                                                   |
| ------ | ---------------------------------------------------------------------- |
| curl   | 用于从或向服务器传输数据，支持多种协议。                               |
| git    | 分布式版本控制系统，用于跟踪和协作开发软件项目的源代码。               |
| htop   | 一个交互式的系统监视器，用于实时查看和管理运行中的进程。               |
| rclone | 用于在本地和云存储之间同步、管理文件的命令行程序，支持多种云存储服务。 |
| rsync  | 用于高效同步和传输文件，支持本地和远程文件。                           |
| s3cmd  | 用于管理 Amazon S3 云存储服务。                                        |
| ssh    | 用于安全地远程访问和管理服务器。                                       |
| unzip  | 用于解压缩ZIP文件。                                                    |
| vim    | 一款高效、可定制的文本编辑器，常用于编程和文本编辑。                   |
| wget   | 用于从网络上下载文件，支持 HTTP、HTTPS 和 FTP 协议。                   |
| zip    | 用于创建和管理ZIP压缩文件。                                            |

## 不再维护的 Notebook 标准镜像

| 名称                           | 主要环境     | 备注     |
| ------------------------------ | ------------ | -------- |
| tensorflow-2.11.0-notebook-cpu | TensorFlow 2 | CPU 镜像 |
| tensorflow-2.11.0-notebook-gpu | TensorFlow 2 | GPU 镜像 |
