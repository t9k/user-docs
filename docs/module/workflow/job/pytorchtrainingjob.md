---
title: PyTorchTrainingJob
---

# PyTorchTrainingJob

PyTorchTrainingJob 是服务于 [PyTorch:octicons-link-external-16:](https://pytorch.org/){target=_blank} 分布式训练框架的 T9k Job。

您可以较为方便地使用 PyTorchTrainingJob 为 PyTorch 训练脚本提供训练环境，并监控训练进程。

## 创建 PyTorchTrainingJob

下面是一个基本的 PyTorchTrainingJob 配置示例：

```yaml
apiVersion: batch.tensorstack.dev/v1beta1
kind: PyTorchTrainingJob
metadata:
  name: pytorch-example
spec:
  replicaSpecs:
  - replicas: 4
    restartPolicy: OnFailure
    template:
      spec:
        containers:
        - command:
          - python
          - dist_mnist.py
          image: pytorch/pytorch:2.0.0-cuda11.7-cudnn8-devel
          name: pytorch
    type: worker
```

在该例中：

* 创建 4 个副本（由 `spec.replicaSpecs[*].replicas` 字段指定），副本的角色为 `worker`（由 `spec.replicaSpecs[*].type` 字段指定）。
* 每个副本使用 `pytorch/pytorch:2.0.0-cuda11.7-cudnn8-devel` 镜像，执行命令 `python dist_mnist.py`（由 `template` 字段指定，此处的填写方式参考 [PodTemplate:octicons-link-external-16:](https://kubernetes.io/docs/concepts/workloads/pods/#pod-templates){target=_blank}）。
* 当副本失败后，会自动重启（由 `spec.replicaSpecs[*].restartPolicy` 字段指定）。

!!! note "注意"
    PyTorchTrainingJob 中执行的脚本应使用 PyTorch 分布式训练框架，否则可能达不到训练效果。

## 使用 torchrun 启动训练

前面的示例中所使用的训练方法比较原始，即直接用 `python` 启动训练脚本，执行训练。

PyTorch 在后续提供了 `torch.distributed.launch` 包和 `torchrun` 工具来更好地启动和管理训练，具体优点包括：支持**一机多进程**、**高容错**、**弹性伸缩训练规模**等。PyTorchTrainingJob 也支持使用 `torchrun` 启动训练来继承这些优点。

```yaml
spec:
  torchrunConfig:
    enable: true
    minNodes: 1
    maxRestarts: 10
    procPerNode: "1"
    rdzvBackend: c10d
    extraOptions: []
```

在 PyTorchTrainingJob 的定义中加入上述片段，来使用 `torchrun` 启动训练，其中：

* `enable`：是否启用 `torchrun`。
* `minNodes`：弹性伸缩训练的最小副本数量。
* `maxRestarts`：训练进程的最多重启次数。
* `procPerNode`：一个副本中启动多少个训练进程。除了可以指定一个数字字符串之外，还可以设置为 `gpu`，表示启动等同于副本所使用的 GPU 数量的训练进程。
* `rdzvBackend`：`torchrun` 所使用的汇合通信方式，可以设置为 `c10d`、`etcd` 或 `etcd-v2`，但是只有 `c10d` 是 `torch` 内置的。如果用户希望使用 `etcd` 需要自行搭建 `etcd` 服务器。
* `extraOptions`：`torchrun` 的其他参数，上面的参数是 `torchrun` 比较常用的设置，用户也可以通过 `extraOptions` 字段提供更多 `torchrun` 的其他设置。

!!! note "注意"
    如果使用 torchrun 启动训练，容器的启动命令变为 `torchrun $torchrun_arg $training_script $training_args` 形式，其中 `training_script` 和 `training_args` 由字段 `spec.replicaSpecs[*].template.spec.containers[0].args` 指定，`spec.replicaSpecs[*].template.spec.containers[0].command` 将不再生效。

    另外，PyTorchTrainingJob 使用 torchrun 前需要确定哪一个容器才是训练容器：如果有一个容器的 `name` 是 `python`，则这个容器是训练容器；否则序号为 0 的容器为训练容器。

### 最佳实践

```yaml
...
spec:
  torchrunConfig:
    enable: false
    minNodes: 1
    maxRestarts: 10
    procPerNode: "1"
    rdzvBackend: c10d
    extraOptions: []
  replicaSpecs:
  - replicas: 4
    restartPolicy: OnFailure
    template:
      spec:
        containers:
        - command:
          - python
          args:
          - dist_mnist.py
          image: pytorch/pytorch:2.0.0-cuda11.7-cudnn8-devel
          name: pytorch
    type: worker
...
```

在上面的示例中：`spec.replicaSpecs[*].template.spec.containers[0].command` 只填写 `python`，其他参数填写在 `spec.replicaSpecs[*].template.spec.containers[0].args` 中。这样可以实现以下效果：

* 当 `spec.torchrunConfig.enable` 设置为 `false` 时，控制器会为训练副本设置正确的环境变量，并通过 `python dist_mnist.py` 命令启动训练脚本。
* 当 `spec.torchrunConfig.enable` 设置为 `true` 时，控制器会忽略 `python` 命令，而是改用 `torchrun` 命令，其格式为：`torchrun <torchrun_args> dist_mnist.py`。

这样做的优点就是，在切换 `torchrun` 模式时，不需要对其他字段进行改动。

另外，如果用户使用 Python Module 作为训练脚本，可以参考以下配置：

```yaml
...
spec:
  torchrunConfig:
    enable: false
    ...
  replicaSpecs:
  - replicas: 4
    restartPolicy: OnFailure
    template:
      spec:
        containers:
        - command:
          - python
          args:
          - -m
          - training.module
          image: pytorch/pytorch:2.0.0-cuda11.7-cudnn8-devel
          name: pytorch
    type: worker
...
```

在上面的示例中，当 `spec.torchrunConfig.enable` 设置为 `true` 时，`-m` 参数同样可以被 `torchrun` 使用。

## 成功和失败

在 PyTorch 分布式训练框架中，需要设置 `MASTER_ADDR` 和 `MASTER_PORT`，PyTorchTrainingJob 会将第一个训练副本作为 master（主节点）。当分布式训练的主节点成功结束，PyTorch 分布式训练成功；反之，当分布式训练的主节点执行失败，PyTorch 分布式训练失败。

但是 master 的失败有时可能是因为环境因素导致的，比如集群网络断连、集群节点崩溃等等，此类原因导致的失败应该被允许自动恢复。针对这一情况，PyTorchTrainingJob 支持副本重启（请参阅[重启机制](#重启机制)），并设定了重启次数限制（由 `spec.runPolicy.backoffLimit` 字段指定），当副本重启次数达到上限后，如果主节点再次失败，则训练失败。此外，PyTorchTrainingJob 可以设置最长执行时间（由 `spec.runPolicy.activeDeadlineSeconds` 字段指定），当超过这个执行时间后，训练失败。

如果 PyTorchTrainingJob 在没有超过重启次数和没有超过最长执行时间的情况下成功完成了主节点的运行，则训练成功。

## 重启机制

PyTorchTrainingJob 的 `spec.replicaSpec[*].template` 字段使用 [PodTemplate:octicons-link-external-16:](https://kubernetes.io/docs/concepts/workloads/pods/#pod-templates){target=_blank} 的规范填写，但是 Pod 的重启策略并不能满足 PyTorchTrainingJob 的需求，所以 PyTorchTrainingJob 使用 `spec.replicaSpec[*].restartPolicy` 字段覆盖 `spec.replicaSpec[*].template` 中指定的重启策略。

可选的重启策略有以下四种：

* `Never`：不重启
* `OnFailure`：失败后重启
* `Always`：总是重启
* `ExitCode`：特殊退出码重启

使用 `Never` 重启策略时，Job 的副本失败后不会重启。如果需要调试代码错误，可以选择此策略，便于从副本中读取训练日志。

`ExitCode` 是一种比较特殊的重启策略，它将失败进程的返回值分为两类：一类是由于系统环境原因或用户操作导致的错误，此类错误可以通过重启解决；另一类是代码错误或者其他不可自动恢复的错误。可重启的退出码包括：

* 130（128+2）：使用 `Control+C` 终止容器运行。
* 137（128+9）：容器接收到 `SIGKILL` 信号。
* 143（128+15）：容器接收到 `SIGTERM` 信号。
* 138：用户可以自定义这个返回值的含义。如果用户希望程序在某处退出并重启，可以在代码中写入这个返回值。

### 重启次数限制

如果因为某种原因（例如代码错误或者环境错误并且长时间没有修复），PyTorchTrainingJob 不断地失败重启却无法解决问题，这会导致集群资源的浪费。用户可以通过设置 `spec.runPolicy.backoffLimit` 字段来设置副本的最大重启次数。重启次数为所有副本共享，即所有副本重启次数累计达到此数值后，副本将不能再次重启。

## 清除策略

在训练结束后，可能有些副本仍处于运行状态。这些运行的副本仍然会占用集群资源，PyTorchTrainingJob 提供清除策略，在训练结束后删除这些副本。

PyTorchTrainingJob 提供以下三种策略：

* `None`：不删除副本。
* `All`：删除所有副本。
* `Unfinished`：只删除未结束的副本。

!!! tip "提示"
    已结束的副本不会继续消耗集群资源，因此在一定程度上，`Unfinished` 策略比 `All` 策略更优。但这并不总是适用，由于一个项目的资源配额的计算不考虑 Pod 是否已经结束，对于资源紧张的项目，如果确定不需要通过日志来调试 Job，则可以使用 `All` 策略。
    
    `None` 策略主要用于训练脚本调试阶段。如果需要从副本中读取训练日志，则可以选用此策略。但由于这些副本可能占用资源并影响后续训练，建议用户在调试完毕后手动删除这些副本或删除整个 PyTorchTrainingJob。

## 调度器

目前 PyTorchTrainingJob 支持使用以下两种调度器：

1. Kubernetes 的[默认调度器:octicons-link-external-16:](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/#kube-scheduler){target=_blank}
2. [T9k Scheduler 调度器](../../cluster/scheduling/index.md)

调度器通过 `spec.scheduler` 字段设置：

* 不设置 `spec.scheduler` 字段，则默认使用 Kubernetes 的默认调度器。
* 设置 `spec.scheduler.t9kScheduler` 字段，则使用 T9k Scheduler 调度器。

在下面的示例中，PyTorchTrainingJob 启用 T9k Scheduler 调度器，将副本插入 `default` 队列中等待调度，其优先级为 50。

```yaml
...
spec:
  scheduler:
    t9kScheduler:
      queue: default
      priority: 50
```

!!! info "信息"
    队列和优先级都是 T9k Scheduler 的概念，具体含义请参阅 [T9k Scheduler](../../cluster/scheduling/index.md)。

## TensorBoard 的使用

PyTorchTrainingJob 支持使用 TensorBoard 对训练过程和结果进行实时可视化（由 `spec.tensorboardSpec` 字段设置）。

在下面的示例中，PyTorchTrainingJob 使用 `t9kpublic/tensorboard:2.11.0` 镜像创建一个 TensorBoard，可视化名为 `torch-tensorboard-pvc` 的 PVC 中 `/log` 路径下的模型数据。

```yaml
...
spec:
  tensorboardSpec:
    image: t9kpublic/tensorboard:2.11.0
    trainingLogFilesets:
    - t9k://pvc/torch-tensorboard-pvc/log
```

!!! info "信息"
    TensorBoard 的详细介绍请参阅 [TensorBoard](../../building/tensorboard.md)。

## Debug 模式

PyTorchTrainingJob 支持 Debug 模式，在该模式下，训练环境会被部署好，但不会启动训练，用户可以连入副本测试环境或脚本。

该模式可以通过 `spec.runMode.debug` 字段来设置：

* `spec.runMode.debug.enable` 表示是否启用 Debug 模式。
* `spec.runMode.debug.replicaSpecs` 表示如何配置各个副本的 Debug 模式：
    * `spec.runMode.debug.replicaSpecs.type` 表示作用于的副本类型。
    * `spec.runMode.debug.replicaSpecs.skipInitContainer` 表示让副本的 InitContainer 失效，默认为 `false`。
    * `spec.runMode.debug.replicaSpecs.command` 表示副本在等待调试的时候执行的命令，默认为 `sleep inf`。
    * 如果不填写 `spec.runMode.debug.replicaSpecs` 字段，则表示副本使用上述默认设置。

在下面的示例中：

* 示例一：开启了 Debug 模式，并配置 worker 跳过 InitContainer，并执行 `/usr/bin/sshd`。
* 示例二：开启了 Debug 模式，副本使用默认 Debug 设置，即不跳过 InitContainer，并执行 `sleep inf`。

```yaml
# 示例一
...
spec:
  runMode:
    debug:
      enable: true
      replicaSpecs:
        - type: worker
          skipInitContainer: true
          command: ["/usr/bin/sshd"]

---
# 示例二
...
spec:
  runMode:
    debug:
      enable: true
```

## 下一步

* 了解如何[使用 PyTorchTrainingJob 进行 PyTorch 分布式训练](../../../guide/run-distributed-training/pytorch/index.md)
