---
title: t9k.ah.core.Tag
---

# t9k.ah.core.Tag

```python
Tag(asset: Union[t9k.ah.core.Model, t9k.ah.core.Dataset], name: str, id_: str)
```

Represents a tag of Asset.

## Attributes

## Ancestors

* `t9k.ah.core._Ref`
* **asset** (*Any*)

    A Model or Dataset instance corresponding to the Asset that the tag belongs to.

* **type** (*Any*)

    A string "tag".

* **id** (*Any*)

    ID of the commit that the tag points to.

* **name** (*str*)

    Name of the tag.

## Methods

### create_tag

```python
create_tag(self, *args, **kwargs)
```

### delete

```python
delete(self, *args, **kwargs)
```

### download

```python
download(self, *args, **kwargs)
```
