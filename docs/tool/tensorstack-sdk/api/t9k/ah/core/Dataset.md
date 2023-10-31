---
title: t9k.ah.core.Dataset
---

# t9k.ah.core.Dataset

```python
Dataset(id_: str, folder: t9k.ah.core.Folder, name: str, labels: List[str], description: str, extra: str)
```

Represents a Dataset in server.

## Attributes

* **path** (*str*)

    Path of the Dataset in server.

* **id** (*str*)

    ID of the Dataset in server.

* **folder** (*t9k.ah.core.Folder*)

    A `Folder` instance corresponding to the Folder that the Dataset belongs to.

* **kind** (*str*)

    A string `'Dataset'`.

* **name** (*str*)

    Name of the Dataset.

* **labels** (*List[str]*)

    Labels of the Dataset.

* **description** (*str*)

    Description of the Dataset.

* **commit_id** (*str*)

    ID of the commit that the main branch points to.

* **extra** (*str*)

    Extra information about the Dataset.

* **alive** (*bool*)

    Whether the Dataset is alive.

## Ancestors

* `t9k.ah.core._Dataset`

## Methods

### create_commit

```python
create_commit(self, msg: str, delete: Optional[Sequence[str]] = None, add: Union[Sequence[str], Mapping[str, str], None] = None) ‑> Optional[t9k.ah.core.Commit]
```

Commits changes to this Dataset.

First delete, then add.

#### Examples

Add a file as object to this Dataset:
```python
dataset.create_commit(msg='add ...', add=['0.png'])
```

Specify a path in Dataset for an object to add:
```python
dataset.create_commit(msg='add ...', add={'0.png': 'data/'})
```

Add all files under a directory as objects:
```python
dataset.create_commit(msg='add ...', add=['./data'])
```

Delete an object from this Dataset:
```python
dataset.create_commit(msg='delete ...', delete=['0.png'])
```

Delete all objects under the specified path:
```python
dataset.create_commit(msg='delete ...', delete=['data/'])
```

#### Args

* **msg** (*str*)

    Commit message.

* **delete** (*Optional[Sequence[str]]*)

    Files or directories to delete from the Dataset, can be a sequence of paths in Dataset or `None`. If empty sequence or `None`, delete nothing. If the files or directories to delete do not exist, do nothing (rather than raise an error). Here format `a/.../b` signifies a file, while `a/.../b/` signifies a directory.

* **add** (*Union[Sequence[str], Mapping[str, str], None]*)

    Files or directories to add to the Dataset, can be a sequence of local paths, a mapping from local paths to their paths in Dataset, or `None`. If empty sequence, empty mapping or `None`, add nothing.

#### Returns

A `Commit` instance representing created commit if changes are
commited, `None` if not.

### delete

```python
delete(self) ‑> None
```

Deletes this Dataset.

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

### get_tag

```python
get_tag(self, name: str, verbose: bool = True) ‑> t9k.ah.core.Tag
```

Gets a tag of this Dataset.

#### Args

* **name** (*str*)

    Name of the tag.

* **verbose** (*bool*)

    Whether to log error.

#### Returns

A `Tag` instance representing retrieved tag.

### list_branch

```python
list_branch(self) ‑> List[Dict[str, Any]]
```

Lists branches in this Dataset.

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

### list_tag

```python
list_tag(self) ‑> List[Dict[str, Any]]
```

Lists tags of this Dataset.

### update

```python
update(self, name: Optional[str] = None, labels: Optional[Sequence[str]] = None, description: Optional[str] = None) ‑> None
```

Updates the metadata of this Dataset.

If none of the args is provided, do nothing.

#### Args

* **name** (*Optional[str]*)

    New name of this Dataset.

* **labels** (*Optional[Sequence[str]]*)

    New labels of this Dataset.

* **description** (*Optional[str]*)

    New description of this Dataset.
