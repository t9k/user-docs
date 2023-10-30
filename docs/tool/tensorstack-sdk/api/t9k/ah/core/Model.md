---
title: t9k.ah.core.Model
---

# t9k.ah.core.Model

```python
Model(id_: str, folder: t9k.ah.core.Folder, name: str, labels: List[str], description: str, extra: str)
```

Represents a Model in server.

## Attributes

## Ancestors

* `t9k.ah.core._Asset`

## Methods

### download

```python
download(self, paths: Optional[Sequence[str]] = None, save_dir: str = '.') ‑> None
```

Downloads objects of this Model.

#### Args

* **paths** (*Optional[Sequence[str]]*)

    Files or directories to download from this Dataset, is a sequence of paths in Dataset. Here format `a/.../b` signifies a file while `a/.../b/` signifies a directory. Defaults to all objects.

* **save_dir** (*str*)

    Local directory which objects are downloaded to. If the directory does not exist, create it. Defaults to current working directory.

### get_branch

```python
get_branch(self, name: str, verbose: bool = True) ‑> t9k.ah.core.Branch
```

Gets a branch of this Model.

#### Args

* **name** (*str*)

    Name of the branch.

* **verbose** (*bool*)

    Whether to log error.

#### Returns

A `Branch` instance representing retrieved branch.

### list_object

```python
list_object(self) ‑> List[Dict[str, Any]]
```

Lists objects of this Model.
