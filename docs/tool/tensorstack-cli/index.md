---
title: TensorStack CLI
---

# TensorStack CLI

TensorStack CLI（简称 T9k CLI）是 TensorStack AI 平台的命令行工具，用于对 TensorStack AI 平台的各种资源对象进行增、删、改、查操作。

!!! info "信息"
    如果您使用过 kubectl，那么您可以将 T9k CLI 看作面向 T9k 资源的 kubectl（但是 T9k CLI 采用了资源对象在前、操作在后的语法格式，如 `t9k notebook get -A`）。这样的类比能帮助您非常快速地理解 T9k CLI 的用法。但是不了解 kubectl 也不会影响您阅读本文档，您可以从本文档中学会 T9k CLI 的使用方式。

## 功能
TensorStack CLI 目前包含了两大功能：其一是管理 T9k 集群资源分配，主要的使用者是 TensorStack AI 平台管理员；其二是管理 TensorStack AI 平台中被创建的任务、训练等资源，主要的使用者是使用平台进行机器学习模型开发、训练、部署等工作的数据科学家。

TensorStack CLI 的目标是：提供对于 T9k 自定义资源的有效支持。对于平台管理员来说，这些功能可以作为 kubectl 的补充来管理 TensorStack AI 平台。对于数据科学家来说，这些功能和网页一起，帮助他们只需要一些 Kubernetes 的基础知识，就可以在 TensorStack AI 平台上开展机器学习相关的工作。

<figure>
  <img alt="architecture" src="../../assets/tool/tensorstack-cli/architecture.drawio.svg"/>
</figure>

<center>图 1：T9k CLI 示意图</center>

## 资源类型

T9k CLI 支持的资源类型分为以下三类：

* 基于 Kubernetes 定义的，用来解决机器学习相关问题的 TensorStack AI 平台资源：
    * AutoTune
    * BeamJob
    * GenericJob
    * MLService
    * MPIJob
    * Notebook
    * PyTorchTrainingJob
    * SimpleMLService
    * TensorFlowTrainingJob
    * WorkflowTemplate
    * WorkflowRun
    * XGBoostTrainingJob
* 基于 Kubernetes 定义的，用来管理集群资源及权限的 TensorStack AI 平台资源：
    * PodGroup
    * Project
    * Queue
* 其他功能。目前只有 Python 程序的容器化：在不依赖 Docker 守护进程的前提下，将 Python 代码打包成一个可以运行的 Docker 镜像。

