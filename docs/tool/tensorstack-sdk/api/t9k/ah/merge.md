---
title: t9k.ah.merge
---

# t9k.ah.merge

```python
merge(path: str) ‑> None
```

Merges a branch of a Model to the main branch.

Here, the specific operation of "merge" involves deleting all objects from the main branch and then copying all objects from the specified branch to the main branch.

Note that the specified branch itself cannot be the main branch.

## Examples

```python
ah.merge('model/llm/gpt2:v1')
```

## Args

* **path** (*str*)

    Path of the branch.
