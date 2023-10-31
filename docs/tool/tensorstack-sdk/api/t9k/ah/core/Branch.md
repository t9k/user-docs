---
title: t9k.ah.core.Branch
---

# t9k.ah.core.Branch

```python
Branch(asset: Union[t9k.ah.core.Model, t9k.ah.core.Dataset], name: str, commit_id: str)
```

Represents a branch of Asset.

## Attributes

* **path** (*str*)

    Path of the branch.

* **asset** (*Union[t9k.ah.core.Model, t9k.ah.core.Dataset]*)

    A `Model` or `Dataset` instance corresponding to the Asset that the branch belongs to.

* **kind** (*str*)

    A string `'branch'`.

* **name** (*str*)

    Name of the branch.

* **commit_id** (*str*)

    ID of the commit that the branch points to.

* **alive** (*bool*)

    Whether the branch is alive.

## Ancestors

* `t9k.ah.core._Ref`

## Methods

### create_commit

```python
create_commit(self, msg: str, delete: Optional[Sequence[str]] = None, add: Union[Sequence[str], Mapping[str, str], None] = None, force: bool = False) ‑> Optional[t9k.ah.core.Commit]
```

Commits changes to this branch.

First delete, then add.

#### Examples

Add a file as object to this branch:
```python
branch.create_commit(msg='add ...', add=['model.pt'])
```

Specify a path in Asset for a file to add:
```python
branch.create_commit(msg='add ...', add={'model.pt': 'saved_model/'})
```

Add all files under a directory as objects (with the directory):
```python
branch.create_commit(msg='add ...', add=['./saved_model'])
```

Add all files under a directory as objects (without the directory):
```python
branch.create_commit(msg='add ...', add=['./saved_model/*'])
```

Specify a path in Asset for a directory to add:
```python
branch.create_commit(msg='add ...', add={'./saved_model': 'path/to/[saved_model]'})
# or
branch.create_commit(msg='add ...', add={'./saved_model': 'path/to/renamed_dir'})
```

Delete an object from this branch:
```python
branch.create_commit(msg='delete ...', delete=['model.pt'])
```

Delete all objects under the specified path:
```python
branch.create_commit(msg='delete ...', delete=['saved_model/'])
```

#### Args

* **msg** (*str*)

    Commit message.

* **delete** (*Optional[Sequence[str]]*)

    Files or directories to delete from the branch, can be a sequence of paths in branch or `None`. If empty sequence or `None`, delete nothing. If the files or directories to delete do not exist, do nothing (rather than raise an error). Here format `a/.../b` signifies a file, while `a/.../b/` signifies a directory.

* **add** (*Union[Sequence[str], Mapping[str, str], None]*)

    Files or directories to add to the branch, can be a sequence of local paths, a mapping from local paths to their paths in Asset, or `None`. If empty sequence, empty mapping or `None`, add nothing.

* **force** (*bool*)

    Whether to create a new commit if unknown changes or unimplemented changes are found.

#### Returns

A `Commit` instance representing created commit if changes are
commited, `None` if not.

### create_tag

```python
create_tag(self, name: str) ‑> t9k.ah.core.Tag
```

Creates a tag that points to this branch.

#### Args

* **name** (*str*)

    Name of the tag.

#### Returns

A `Tag` instance representing created tag.

### delete

```python
delete(self) ‑> None
```

Deletes this branch.

### download

```python
download(self, paths: Optional[Sequence[str]] = None, save_dir: str = '.') ‑> None
```

Downloads objects of this branch.

#### Args

* **paths** (*Optional[Sequence[str]]*)

    Files or directories to download from this branch, is a sequence of paths in branch. Here format `a/.../b` signifies a file while `a/.../b/` signifies a directory. Defaults to all objects.

* **save_dir** (*str*)

    Local directory which objects are downloaded to. If the directory does not exist, create it. Defaults to current working directory.


### get_commit

```python
get_commit(self, index: Optional[int] = None, id: Optional[str] = None) ‑> t9k.ah.core.Commit
```

Gets a commit of this branch.

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

Lists commits of this branch.

### list_object

```python
list_object(self) ‑> List[Dict[str, Any]]
```

Lists objects of this branch.

### merge

```python
merge(self) ‑> None
```

Merges this branch to the main branch.

Here, the specific operation of "merge" involves deleting all objects
from the main branch and then copying all objects from this branch to
the main branch.

Note that this branch itself cannot be the main branch.

### reset

```python
reset(self) ‑> None
```

Resets this branch to clear all uncommitted changes.
