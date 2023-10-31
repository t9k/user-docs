---
title: t9k.ah.core.Tag
---

# t9k.ah.core.Tag

```python
Tag(asset: Union[t9k.ah.core.Model, t9k.ah.core.Dataset], name: str, commit_id: str)
```

Represents a tag of Asset.

## Attributes

* **path** (*str*)

    Path of the tag.

* **asset** (*Union[t9k.ah.core.Model, t9k.ah.core.Dataset]*)

    A `Model` or `Dataset` instance corresponding to the Asset that the tag belongs to.

* **kind** (*str*)

    A string `'tag'`.

* **name** (*str*)

    Name of the tag.

* **commit_id** (*str*)

    ID of the commit that the tag points to.

* **alive** (*bool*)

    Whether the tag is alive.

## Ancestors

* `t9k.ah.core._Ref`

## Methods

### create_tag

```python
create_tag(self, name: str) ‑> t9k.ah.core.Tag
```

Creates another tag that points to this tag.

#### Args

* **name** (*str*)

    Name of the tag.

#### Returns

A `Tag` instance representing created tag.

### delete

```python
delete(self) ‑> None
```

Deletes this tag.

### download

```python
download(self, paths: Optional[Sequence[str]] = None, save_dir: str = '.') ‑> None
```

Downloads objects of this tag.

#### Args

* **paths** (*Optional[Sequence[str]]*)

    Files or directories to download from this tag, is a sequence of paths in tag. Here format `a/.../b` signifies a file while `a/.../b/` signifies a directory. Defaults to all objects.

* **save_dir** (*str*)

    Local directory which objects are downloaded to. If the directory does not exist, create it. Defaults to current working directory.


### list_commit

```python
list_commit(self) ‑> List[Dict[str, Any]]
```

Lists commits of this tag.

### list_object

```python
list_object(self) ‑> List[Dict[str, Any]]
```

Lists objects of this tag.
