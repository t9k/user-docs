---
title: t9k.ah.core.Model
---

# t9k.ah.core.Model

```python
Model(id_: str, folder: t9k.ah.core.Folder, name: str, labels: List[str], description: str, extra: str)
```

Represents a Model in server.

## Attributes

* **path** (*str*)

    Path of the Model in server.

* **id** (*str*)

    ID of the Model in server.

* **folder** (*t9k.ah.core.Folder*)

    A `Folder` instance corresponding to the Folder that the Model belongs to.

* **kind** (*str*)

    A string `'Model'`.

* **name** (*str*)

    Name of the Model.

* **labels** (*List[str]*)

    Labels of the Model.

* **description** (*str*)

    Description of the Model.

* **extra** (*str*)

    Extra information about the Model.

* **alive** (*bool*)

    Whether the Model is alive.

## Ancestors

* `t9k.ah.core._Model`

## Methods

### create_branch

```python
create_branch(self, name: str) ‑> t9k.ah.core.Branch
```

Creates an empty branch of this Model.

#### Args

* **name** (*str*)

    Name of the branch.

#### Returns

A `Branch` instance representing created branch.

### delete

```python
delete(self) ‑> None
```

Deletes this Model.

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

### get_commit

```python
get_commit(self, id: str) ‑> t9k.ah.core.Commit
```

Gets a commit of this Model.

If no commit matches `id`, or two or more commits matche `id`,
raise a `RuntimeError`.

#### Args

* **id** (*str*)

    A prefix of ID of the commit.

#### Returns

A `Commit` instance representing retrieved commit.

### get_tag

```python
get_tag(self, name: str, verbose: bool = True) ‑> t9k.ah.core.Tag
```

Gets a tag of this Model.

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

Lists branches in this Model.

### list_object

```python
list_object(self) ‑> List[Dict[str, Any]]
```

Lists objects of this Model.

### list_tag

```python
list_tag(self) ‑> List[Dict[str, Any]]
```

Lists tags of this Model.

### update

```python
update(self, name: Optional[str] = None, labels: Optional[Sequence[str]] = None, description: Optional[str] = None) ‑> None
```

Updates the metadata of this Model.

If none of the args is provided, do nothing.

#### Args

* **name** (*Optional[str]*)

    New name of this Model.

* **labels** (*Optional[Sequence[str]]*)

    New labels of this Model.

* **description** (*Optional[str]*)

    New description of this Model.
