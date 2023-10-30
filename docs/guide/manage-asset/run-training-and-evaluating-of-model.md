---
title: 运行模型的训练和评估
---

# 运行模型的训练和评估

本教程演示，以及如何通过多种方式运行模型的训练和评估。

## 准备工作

* 完成教程[操作 Asset 的对象](./manipulate-object-of-asset.md)。
* 完成教程[管理模型的评估结果](./manage-evaluation-of-model.md)。

## 准备一套模型训练/评估代码

## 通过命令行工具

切换到您的工作路径下：

```shell
$ cd /your/workpath
```

依次创建 Model Folder 和 Model：

```shell
$ ah create folder model/image-classification
AH INFO: Creating Model Folder image-classification

$ ah create model image-classification/mnist-cnn-keras
AH INFO: Creating Model mnist-cnn-keras in Folder image-classification
```

使用 `ah train` 命令启动一次训练，指定上文中准备的模型训练/评估代码，指定一个 Dataset 作为训练集，给定 100MiB 的临时存储空间以用于训练。最终训练保存的模型文件会存储到名为 `epoch-5` 的新分支中：

```shell
$ ah train image-classification/mnist-cnn-keras -b epoch-5 -d image-classification/mnist -v 100Mi -r https://github.com/user/repo -i master -s mnist
AH INFO: Training with codes https://github.com/user/repo and dataset mnist
AH INFO: Generated model files will be saved to branch epoch-5 of Model mnist-cnn-keras
```

使用 `ah ls workflow` 命令查看 Model 的所有工作流（上面启动的训练以及下面将要启动的评估实质上都是 [WorkflowRun](../../module/workflow/workflow/workflowrun.md)）：

```shell
$ ah ls workflow image-classification/mnist-cnn-keras                                
ID:             986a15a6-6c61-44f8-9d93-1df6d16933da
TYPE:           train
NAME:           asset-hub-pdhg9
GIT_REPO:       https://github.com/user/repo
GIT_REVISION:   master
GIT_SUBPATH:    mnist
DATASET:        user/dataset/image-classification/mnist:main
TARGET_BRANCH:  epoch-5
STATUS:         Running
STARTED:        37s ago
```

等待数分钟后训练完成（工作流的状态变为 `Succeeded`），使用 `ah ls object` 命令查看保存的模型文件：

```shell
$ ah ls object model/image-classification/mnist-cnn-keras:epoch-5
PATH                   BYTES  CHECKSUM                          MODIFIED
asset-hub.metadata      230B  2d17722a547e0de02bfe9329b63d88eb  5m29s ago
model_state_dict.pt  375943B  201a5a86ca4c578ae3299f98fdf0031b  5m37s ago
```

其中 `asset-hub.metadata` 文件记录了该次训练的部分参数。

再次使用 `ah train` 命令启动一次继续训练，指定前一次训练保存的模型文件作为检查点（`epoch-5` 分支中的 `model_state_dict.pt` 文件），在其基础上进行训练，其他参数（除分支名外）保持不变：

```shell
$ ah train image-classification/mnist-cnn-keras -b epoch-10 -d image-classification/mnist -v 100Mi -r https://github.com/user/repo -i master -s mnist -c image-classification/mnist-cnn-keras:epoch-5
AH INFO: Continue training commit 47a530c6 with codes https://github.com/user/repo and dataset mnist
AH INFO: Generated model files will be saved to branch epoch-10 of Model mnist-cnn-keras
```

使用 `ah evaluate` 命令启动一次评估，指定第一次（或第二次）训练保存的模型文件作为检查点，对其进行评估，其他参数（使用的代码、数据集等）和上面相同：

```shell
$ ah evaluate image-classification/mnist-cnn-keras:epoch-5 -d image-classification/mnist -v 100Mi -r https://github.com/user/repo -i master -s mnist
```

等待数分钟后评估完成，使用 `ah ls evaluation` 命令查看该评估的结果：

```shell
$ ah ls evaluation image-classification/mnist-cnn-keras:epoch-5
ID:              c5c3a09d-676d-40cf-968a-5ef5f211a4eb
MODEL:           user/model/image-classification/mnist-cnn-keras:epoch-5
MODEL_COMMIT:    47a530c6645440a7ef009e306d928059678f02531cb2064535f9c6baad6af605
DATASET:         user/dataset/image-classification/mnist:main
DATASET_COMMIT:  3dda9345975c4d7318f76613dd6255281cc09b79026a4feb41ca0cab5b295d15
UPLOADED:        4m6s ago
RESULTS:         key     value
                 metric  {"loss": 1.473171865940094, "accuracy": 0.9883}
```

## 通过 Python SDK

切换到您的工作路径下，然后以任意方式执行下面的 Python 代码。

导入 `t9k.ah` 模块，使用 `ah.login()` 函数登录到 Asset Hub 服务器（如果配置文件中的凭据仍有效，则无需提供参数）：

```python
from t9k import ah

ah.login(host='<asset-hub-server-url>',
         api_key='<your-api-key>')
```

```
AH INFO: Logged in to Asset Hub server <asset-hub-server-url> as user <your-user-name>
```

依次创建 Model Folder 和 Model：

```python
model_folder = ah.create_folder(type_='model', name='image-classification')
model = model_folder.create_asset(name='mnist-cnn-keras')
```

```
AH INFO: Creating Model Folder image-classification
AH INFO: Creating Model mnist-cnn-keras in Folder image-classification
```

使用 `Model` 实例的 `train()` 方法启动一次训练，指定上文中准备的模型训练/评估代码，指定一个 Dataset 作为训练集，给定 100MiB 的临时存储空间以用于训练。最终训练保存的模型文件会存储到名为 `epoch-5` 的新分支中：

```python
dataset = ah.get_folder(type_='dataset',
                        name='image-classification').get_asset(name='mnist')

model.train(branch='epoch-5',
            dataset=dataset,
            volume='100Mi',
            git_repo='https://github.com/user/repo',
            git_revision='master',
            git_subpath='mnist')
```

```
AH INFO: Training with codes https://github.com/user/repo and dataset mnist
AH INFO: Generated model files will be saved to branch epoch-5 of Model mnist-cnn-keras
```

使用 `Model` 实例的 `list_workflow()` 方法查看 Model 的所有工作流（上面启动的训练以及下面将要启动的评估实质上都是 [WorkflowRun](../../module/workflow/workflow/workflowrun.md)）：

```python
[{'branch': 'epoch-5',
  'dataset': 'user/dataset/image-classification/mnist:main',
  'git_repo': 'https://github.com/user/repo',
  'git_revision': 'master',
  'git_subpath': 'mnist',
  'name': 'asset-hub-c87nd',
  'start_time': '2022-12-01T10:32:48Z',
  'status': 'Running',
  'type': 'train'}]
```

等待数分钟后训练完成（工作流的状态变为 `Succeeded`），使用 `Branch` 实例的 `list_object()` 方法查看保存的模型文件：

```python
branch = model.get_branch(name='epoch-5')
pprint(branch.list_object())
```

```
[{'checksum': 'bfef1951fcc931b01facf927e2814c68',
  'content_type': 'application/octet-stream',
  'mtime': 1669891757,
  'path': 'asset-hub.metadata',
  'path_type': 'object',
  'physical_address': 's3://t9k/35c3b845-9bd2-405a-8c79-f3dbca75269f/24b5f46dfd874d4dabadfff4e1a71e97',
  'size_bytes': 210},
 {'checksum': '3ae7f2fbe98e6546b81051c8c924da8c',
  'content_type': 'application/octet-stream',
  'mtime': 1669891751,
  'path': 'model_state_dict.pt',
  'path_type': 'object',
  'physical_address': 's3://t9k/35c3b845-9bd2-405a-8c79-f3dbca75269f/57b96b10ba4a477cad464dcec8d2073c',
  'size_bytes': 375943}]
```

其中 `asset-hub.metadata` 文件记录了该次训练的部分参数。

再次使用 `Model` 实例的 `train()` 方法启动一次继续训练，指定前一次训练保存的模型文件作为检查点（`epoch-5` 分支中的 `model_state_dict.pt` 文件），在其基础上进行训练，其他参数（除分支名外）保持不变：

```python
model.train(branch='epoch-10',
            dataset=dataset,
            checkpoint=branch,
            volume='100Mi',
            git_repo='https://github.com/user/repo',
            git_revision='master',
            git_subpath='mnist')
```

```
AH INFO: Continue training commit b27858a3 with codes https://github.com/user/repo and dataset mnist
AH INFO: Generated model files will be saved to branch epoch-10 of Model mnist-cnn-keras
```

使用 `Branch` 实例（或 `Tag`、`Commit` 实例）的 `evaluate` 命令启动一次评估，对第一次（或第二次）训练保存的模型文件作为检查点，对其进行评估，其他参数（使用的代码、数据集等）和上面相同：

```python
branch.evaluate(dataset=dataset,
                volume='100Mi',
                git_repo='https://github.com/user/repo',
                git_revision='master',
                git_subpath='mnist')
```

```
AH INFO: Evaluating commit b27858a3 of Model mnist-cnn-keras with codes https://github.com/user/repo and dataset mnist
```

等待数分钟后评估完成，使用 `Branch` 实例（或 `Tag`、`Commit` 实例）的 `list_evaluation()` 方法查看该评估的结果：

```python
pprint(branch.list_evaluation())
```

```
[{'datasetBranch': 'main',
  'datasetCommit': '3dda9345975c4d7318f76613dd6255281cc09b79026a4feb41ca0cab5b295d15',
  'datasetID': '308eacc4-6a95-4301-acc3-2b75ec1e5172',
  'datasetRef': 'user/dataset/image-classification/mnist:main',
  'datasetTags': [],
  'id': '33bb61c6-431b-4129-9769-41ffd79cbf93',
  'modelBranch': 'epoch-5',
  'modelCommit': 'b27858a3664e74443089f10b0fdeb8ce5de3adb7a34e6703233d125426762b45',
  'modelID': '35c3b845-9bd2-405a-8c79-f3dbca75269f',
  'modelRef': 'user/model/image-classification/mnist-cnn-keras:branch/epoch-5',
  'modelTags': [],
  'results': {'metric': '{"loss": 1.4753540992736816, "accuracy": 0.9858}'},
  'startTime': '2022-12-01T11:05:00.303336Z'}]
```

## 通过控制台
