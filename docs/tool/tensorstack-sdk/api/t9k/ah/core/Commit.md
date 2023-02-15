---
title: t9k.ah.core.Commit
---

# t9k.ah.core.Commit

```python
Commit(asset: Union[t9k.ah.core.Model, t9k.ah.core.Dataset], id_: str)
```

Represents a commit of Asset.

## Attributes

## Ancestors

* `t9k.ah.core._Ref`

## Methods

### create_tag

```python
create_tag(self, name: str) ‑> t9k.ah.core.Tag
```

Creates a tag that points to this commit.

#### Args

* **name** (*str*)

    Name of the tag.

#### Returns

A `Tag` instance representing created tag.

### download

```python
download(self, paths: Optional[Sequence[str]] = None, save_dir: str = '.') ‑> None
```

Downloads objects of this commit.

#### Args

* **paths** (*Optional[Sequence[str]]*)

    Files or directories to download from the commit, is a sequence of paths in commit. Here format `a/.../b` signifies a file while `a/.../b/` signifies a directory. Defaults to all objects.

* **save_dir** (*str*)

    Local directory which objects are downloaded to. If directory does not exist, create it. Defaults to current working directory.
