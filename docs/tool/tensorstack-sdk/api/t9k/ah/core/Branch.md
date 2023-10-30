---
title: t9k.ah.core.Branch
---

# t9k.ah.core.Branch

```python
Branch(asset: Union[t9k.ah.core.Model, t9k.ah.core.Dataset], name: str, commit_id: str)
```

Represents a branch of Asset.

## Attributes

* **path** (*Any*)

    Path of the branch.

* **asset** (*Any*)

    A `Model` or `Dataset` instance corresponding to the Asset that the branch belongs to.

* **kind** (*Any*)

    A string `'branch'`.

* **name** (*Any*)

    Name of the branch.

* **commit_id** (*str*)

    ID of the commit that the branch points to.

* **alive** (*Any*)

    Whether the branch is alive.

## Ancestors

* `t9k.ah.core._Ref`

## Methods

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
