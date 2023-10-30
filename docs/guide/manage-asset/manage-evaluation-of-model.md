---
title: 管理模型的评估结果
---

# 管理模型的评估结果

本教程演示如何通过多种方式管理模型的评估结果，包括创建、查看和删除模型的某一个 commit 的评估结果。

## 准备工作

* 完成教程[操作 Asset 的分支、tag 和 commit](./manipulate-branch-tag-and-commit-of-asset.md)。

## 通过命令行工具

切换到您的工作路径下：

```shell
$ cd /your/workpath
```

依次创建 Model Folder、Model 和分支：

```shell
$ ah create folder model/image-classification
AH INFO: Creating Model Folder image-classification

$ ah create model image-classification/mnist-cnn-keras
AH INFO: Creating Model mnist-cnn-keras in Folder image-classification

$ ah create branch image-classification/mnist-cnn-keras:v1
AH INFO: Creating branch v1 of Model mnist-cnn-keras
```

现在 `mnist-cnn-keras` 模型的 `v1` 分支是一个空分支，但作为演示，我们假设其中存储了训练得到的模型（权重）文件，通过在数据集 `image-classification/mnist` 上进行评估，得到了该模型的评估指标 `loss=1.47, accuracy=0.99`。使用 `ah create evaluation` 命令创建该模型的一个评估结果：

```shell
$ ah create evaluation image-classification/cnn-keras:branch/v1 -d image-classification/mnist -m loss=1.47 -m accuracy=0.99
AH INFO: Creating evaluation of commit 4d6988c3 of Model cnn-keras
```

!!! note "注意"
    不管 `ah create evaluation` 命令的参数是何种 Git reference（分支、tag 或 commit），创建的评估结果都是绑定在其当前所指向的 commit 上。

使用 `ah ls evaluation` 命令查看该模型的评估结果：

```shell
$ ah ls evaluation image-classification/cnn-keras:4d6988c3
ID:              2c0b7cef-1db5-4e41-b8ea-5490fd81d4e5
MODEL:           user/model/image-classification/mnist-cnn-keras:branch/cli1
MODEL_COMMIT:    4d6988c3c50ed4954b645ae27820b22d902f8fd09d5fe5fae4cd1c0961d0f706
DATASET:         user/dataset/image-classification/mnist:main
DATASET_COMMIT:  3dda9345975c4d7318f76613dd6255281cc09b79026a4feb41ca0cab5b295d15
UPLOADED:        4m5s ago
RESULTS:         key     value
                 metric  {"acc": "0.99", "loss": "1.47"}
```

最后使用 `ah delete evaluation` 命令删除创建评估结果：

```shell
$ ah delete evaluation 2c0b7cef-1db5-4e41-b8ea-5490fd81d4e5
AH INFO: Deleting evaluation with ID 2c0b7cef-1db5-4e41-b8ea-5490fd81d4e5
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

依次创建 Model Folder、Model 和分支：

```python
model_folder = ah.create_folder(type_='model', name='image-classification')
model = model_folder.create_asset(name='mnist-cnn-keras')
branch = model.create_branch(name='v1')
```

```
AH INFO: Creating Model Folder image-classification
AH INFO: Creating Model mnist-cnn-keras in Folder image-classification
AH INFO: Creating branch v1 of Model mnist-cnn-keras
```

现在 `mnist-cnn-keras` 模型的 `v1` 分支是一个空分支，但作为演示，我们假设其中存储了训练得到的模型（权重）文件，通过在数据集 `image-classification/mnist` 上进行评估，得到了该模型的评估指标 `loss=1.47, accuracy=0.99`。使用 `Branch` 实例的 `create_evaluation()` 方法创建该模型的一个评估结果：

```python
dataset = ah.get_folder(type_='dataset',
                        name='image-classification').get_asset(name='mnist')

branch.create_evaluation(metrics={
    'loss': 1.47,
    'accuracy': 0.99
},
                         dataset=dataset)
```

```
AH INFO: Creating evaluation of commit 07795982 of Model mnist-cnn-keras
```

使用 `Branch` 实例的 `list_evaluation()` 方法查看该模型的评估结果：

```python
from pprint import pprint

pprint(branch.list_evaluation())
```

```
[{'datasetBranch': 'main',
  'datasetCommit': '3dda9345975c4d7318f76613dd6255281cc09b79026a4feb41ca0cab5b295d15',
  'datasetID': '308eacc4-6a95-4301-acc3-2b75ec1e5172',
  'datasetRef': 'user/dataset/image-classification/mnist:main',
  'datasetTags': [],
  'id': '062d92a1-ed93-43f5-a905-2906a2e6b81c',
  'modelBranch': 'v1',
  'modelCommit': '077959828f6cbcaa9a043a60feeb968f0c2a5b6caba6a5da9e6fee3b836e4c83',
  'modelID': '122bf63b-2766-496e-816c-217dc834e258',
  'modelRef': 'user/model/image-classification/mnist-cnn-keras:branch/v1',
  'modelTags': [],
  'results': {'metric': '{"loss": 1.47, "accuracy": 0.99}'},
  'startTime': '2022-12-01T07:21:22.85489Z'}]
```

最后使用 `delete_evaluation()` 函数删除评估结果：

```python
ah.delete_evaluation(evaluation_id='062d92a1-ed93-43f5-a905-2906a2e6b81c')
```

```
AH INFO: Deleting evaluation with ID 062d92a1-ed93-43f5-a905-2906a2e6b81c
```

## 通过控制台
