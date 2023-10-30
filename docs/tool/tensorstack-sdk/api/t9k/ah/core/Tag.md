---
title: t9k.ah.core.Tag
---

# t9k.ah.core.Tag

```python
Tag(asset: Union[t9k.ah.core.Model, t9k.ah.core.Dataset], name: str, commit_id: str)
```

Represents a tag of Asset.

## Attributes

* **path** (*Any*)

    Path of the tag.

* **asset** (*Any*)

    A `Model` or `Dataset` instance corresponding to the Asset that the tag belongs to.

* **kind** (*Any*)

    A string `'tag'`.

* **name** (*Any*)

    Name of the tag.

* **commit_id** (*str*)

    ID of the commit that the tag points to.

* **alive** (*Any*)

    Whether the tag is alive.

## Ancestors

* `t9k.ah.core._Ref`

## Methods

### delete

```python
delete(self) ‑> None
```

Deletes this tag.
