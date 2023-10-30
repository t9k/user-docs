---
title: t9k.ah.get
---

# t9k.ah.get

```python
get(path: str) ‑> Union[t9k.ah.core.Folder, t9k.ah.core.Model, t9k.ah.core.Dataset, t9k.ah.core.Branch, t9k.ah.core.Tag, t9k.ah.core.Commit]
```

Gets a resource.

To get a commit, please provide a commit ID with a length of at least 4 to avoid potential conflicts with branches or tags.

## Examples

Get a Folder:
```python
folder = ah.get('model/llm')
```

Get a Model:
```python
model = ah.get('model/llm/gpt2')
```

Get a Dataset:
```python
dataset = ah.get('dataset/images/cifar10')
```

Get a non-main branch of specified Model:
```python
branch = ah.get('model/llm/gpt2:v1')
```

Get a tag:
```python
tag = ah.get('model/llm/gpt2:20220101')
```

Get another user's Folder:
```python
folder = ah.get('/user/t9k-assethub/model/llm')
```

## Args

* **path** (*str*)

    Path of the resource.

## Returns

A instance representing retrieved resource.
