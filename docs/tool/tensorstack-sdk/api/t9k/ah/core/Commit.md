---
title: t9k.ah.core.Commit
---

# t9k.ah.core.Commit

```python
Commit(asset: Union[t9k.ah.core.Model, t9k.ah.core.Dataset], id_: str)
```

Represents a commit of Asset.

## Attributes

* **path** (*str*)

    Path of the commit.

* **asset** (*Union[t9k.ah.core.Model, t9k.ah.core.Dataset]*)

    A `Model` or `Dataset` instance corresponding to the Asset that the commit belongs to.

* **kind** (*str*)

    A string `'commit'`.

* **name** (*str*)

    First 8 characters of ID of the commit.

* **id** (*str*)

    ID of the commit.

* **alive** (*bool*)

    Whether the commit is alive.

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

    Files or directories to download from this commit, is a sequence of paths in commit. Here format `a/.../b` signifies a file while `a/.../b/` signifies a directory. Defaults to all objects.

* **save_dir** (*str*)

    Local directory which objects are downloaded to. If the directory does not exist, create it. Defaults to current working directory.

### list_commit

```python
list_commit(self) ‑> List[Dict[str, Any]]
```

Lists commits of this commit.

### list_object

```python
list_object(self) ‑> List[Dict[str, Any]]
```

Lists objects of this commit.

