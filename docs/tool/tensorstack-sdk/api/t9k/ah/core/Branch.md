---
title: t9k.ah.core.Branch
---

# t9k.ah.core.Branch

```python
Branch(asset: Union[t9k.ah.core.Model, t9k.ah.core.Dataset], name: str, id_: str)
```

Represents a branch of Asset.

## Attributes

## Ancestors

* `t9k.ah.core._Ref`
* **asset** (*Any*)

    A Model or Dataset instance corresponding to the Asset that the branch belongs to.

* **type** (*Any*)

    A string "branch".

* **id** (*Any*)

    ID of the commit that the branch points to.

* **name** (*str*)

    Name of the branch.

## Methods

### create_commit

```python
create_commit(self, *args, **kwargs)
```

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

### get_commit

```python
get_commit(self, *args, **kwargs)
```

### list_commit

```python
list_commit(self, *args, **kwargs)
```
