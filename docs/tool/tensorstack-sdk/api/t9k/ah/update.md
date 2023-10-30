---
title: t9k.ah.update
---

# t9k.ah.update

```python
update(path: str, name: Optional[str] = None, labels: Optional[Sequence[str]] = None, description: Optional[str] = None) ‑> None
```

Updates a resource.

Only Folders and Assets can be updated.

If none of the args is provided, do nothing.

## Examples

Rename a Folder:
```python
ah.update('model/llm', name='generative-language-model')
```

Relabel a Model:
```python
ah.update('model/llm/gpt2', labels=['JAX'])
```

## Args

* **name** (*Optional[str]*)

    New name of the resource.

* **labels** (*Optional[Sequence[str]]*)

    New labels of the resource.

* **description** (*Optional[str]*)

    New description of the resource.
