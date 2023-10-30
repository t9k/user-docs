---
title: t9k.ah.delete
---

# t9k.ah.delete

```python
delete(path: str, force: bool = False) ‑> None
```

Deletes a resource.

## Examples

Delete a Folder:
```python
ah.delete('model/llm')
```

Delete a Model:
```python
ah.delete('model/llm/gpt2')
```

Delete a Dataset:
```python
ah.delete('dataset/images/cifar10')
```

Delete a non-main branch of specified Model:
```python
ah.delete('model/llm/gpt2:v1')
```

Delete a tag:
```python
ah.delete('model/llm/gpt2:20220101')
```

Delete another user's Folder:
```python
ah.delete('/user/t9k-assethub/model/llm')
```

If the Folder does not exist, do nothing:
```python
ah.delete('model/llm', force=True)
```

## Args

* **path** (*str*)

    Path of the resource.

* **force** (*bool*)

    If True, ignore non-existent resources.
