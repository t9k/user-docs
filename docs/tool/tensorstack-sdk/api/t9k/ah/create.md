---
title: t9k.ah.create
---

# t9k.ah.create

```python
create(path: str, labels: Optional[Sequence[str]] = None, description: str = '', exist_ok: bool = False, create_tag: bool = False, source: str = 'main') ‑> Union[t9k.ah.core.Folder, t9k.ah.core.Model, t9k.ah.core.Dataset, t9k.ah.core.Branch, t9k.ah.core.Tag]
```

Creates a resource.

Note that you cannot create a Folder for another user.

## Examples

Create a Folder:
```python
folder = ah.create('model/llm')
```

Create a Model with labels:
```python
model = ah.create('model/llm/gpt2', labels=['PyTorch'])
```

Create a Dataset with a description:
```python
description = 'CIFAR-10 is a widely used benchmark dataset ...'
dataset = ah.create('dataset/images/cifar10', description=description)
```

Create a non-main branch of specified Model:
```python
branch = ah.create('model/llm/gpt2:v1')
```

Create a tag:
```python
tag = ah.create('model/llm/gpt2:20220101', create_tag=True, source='v1')
# or
tag = ah.create('model/llm/gpt2:20220101', create_tag=True, source='model/llm/gpt2:v1')
```

Create a Model for another user:
```python
model = ah.create('/user/t9k-assethub/model/llm/gpt2')
```

## Args

* **path** (*str*)

    Path of the resource.

* **labels** (*Optional[Sequence[str]]*)

    Labels of the resource. Only applicable for creating a Folder, Model or Dataset.

* **description** (*str*)

    Description of the resource. Only applicable for creating a Folder, Model or Dataset.

* **exist_ok** (*bool*)

    If True and the resource already exists, return a corresponding instance representing the resource; if False and resource exists, raise a `RuntimeError`. Only applicable for creating a Folder, Model or Dataset.

* **create_tag** (*bool*)

    Whether to create a tag instead of a branch. Only applicable for creating a branch or tag.

* **source** (*str*)

    Name/ID or path of the source reference (branch, tag or commit) from which a tag is created. Only applicable for creating a tag.

## Returns

A corresponding instance representing retrieved resource.
