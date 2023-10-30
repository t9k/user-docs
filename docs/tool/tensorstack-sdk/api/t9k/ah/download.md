---
title: t9k.ah.download
---

# t9k.ah.download

```python
download(path: str, objects: Optional[Sequence[str]] = None, save_dir: str = '.')
```

Download objects of a reference of an Asset.

If no reference is provided, `:main` will be used.

## Examples

Download all objects of specified branch of Model to current working directory:
```python
ah.download('model/llm/gpt2:v1')
```

Download an object to specified directory:
```python
ah.download('model/llm/gpt2:v1', objects=['model.pt'], save_dir='./saved_model')
```

Download all objects under the same path:
```python
ah.download('model/llm/gpt2:v1', objects=['saved_model/'])
```

Specify the reference by tag:
```python
ah.download('dataset/images/cifar10:20220101')
```

Specify the reference by commit:
```python
ah.download('dataset/images/cifar10:a41ac4ec')
```

## Args

* **path** (*str*)

    Path of the reference from which objects are downloaded.

* **objects** (*Optional[Sequence[str]]*)

    Objects to download.

* **save_dir** (*str*)

    Local directory which objects are downloaded to.
