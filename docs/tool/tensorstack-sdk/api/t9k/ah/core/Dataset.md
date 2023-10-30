---
title: t9k.ah.core.Dataset
---

# t9k.ah.core.Dataset

```python
Dataset(id_: str, folder: t9k.ah.core.Folder, name: str, labels: List[str], description: str, extra: str)
```

Represents a Dataset in server.

## Attributes

* **path** (*Any*)

    Path of the Dataset in server.

* **id** (*Any*)

    ID of the Dataset in server.

* **folder** (*Any*)

    A `Folder` instance corresponding to the Folder that the Dataset belongs to.

* **kind** (*Any*)

    A string `'Dataset'`.

* **name** (*Any*)

    Name of the Dataset.

* **labels** (*Any*)

    Labels of the Dataset.

* **description** (*Any*)

    Description of the Dataset.

* **commit_id** (*str*)

    ID of the commit that the main branch points to.

* **extra** (*Any*)

    Extra information about the Dataset.

* **alive** (*Any*)

    Whether the Dataset is alive.

## Ancestors

* `t9k.ah.core._Asset`

## Methods

### download

```python
download(self, paths: Optional[Sequence[str]] = None, save_dir: str = '.') ‑> None
```

Downloads objects of this Dataset.

#### Args

* **paths** (*Optional[Sequence[str]]*)

    Files or directories to download from this Dataset, is a sequence of paths in Dataset. Here format `a/.../b` signifies a file while `a/.../b/` signifies a directory. Defaults to all objects.

* **save_dir** (*str*)

    Local directory which objects are downloaded to. If the directory does not exist, create it. Defaults to current working directory.

### get_commit

```python
get_commit(self, index: Optional[int] = None, id: Optional[str] = None) ‑> t9k.ah.core.Commit
```

Gets a commit of this Dataset.

If neither `index` or `id` is provided, return the last commit. If both
`index` and `id` are provided, `id` will not be used.

#### Args

* **index** (*Optional[int]*)

    Index of the commit in this branch, `0` for the last commit, `-1` for the first commit.

* **id** (*Optional[str]*)

    A prefix of ID of the commit.

#### Returns

A `Commit` instance representing retrieved commit.

### list_commit

```python
list_commit(self) ‑> List[Dict[str, Any]]
```

Lists commits of this Dataset.

### list_object

```python
list_object(self) ‑> List[Dict[str, Any]]
```

Lists objects of this Dataset.
