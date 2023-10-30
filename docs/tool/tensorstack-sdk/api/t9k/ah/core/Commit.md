---
title: t9k.ah.core.Commit
---

# t9k.ah.core.Commit

```python
Commit(asset: Union[t9k.ah.core.Model, t9k.ah.core.Dataset], id_: str)
```

Represents a commit of Asset.

## Attributes

* **path** (*Any*)

    Path of the commit.

* **asset** (*Any*)

    A `Model` or `Dataset` instance corresponding to the Asset that the commit belongs to.

* **kind** (*Any*)

    A string `'commit'`.

* **name** (*Any*)

    First 8 characters of ID of the commit.

* **id** (*str*)

    ID of the commit.

* **alive** (*Any*)

    Whether the commit is alive.

## Ancestors

* `t9k.ah.core._Ref`

## Methods
