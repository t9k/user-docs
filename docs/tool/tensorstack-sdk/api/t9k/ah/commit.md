---
title: t9k.ah.commit
---

# t9k.ah.commit

```python
commit(path: str, msg: str, delete: Optional[Sequence[str]] = None, add: Union[Sequence[str], Mapping[str, str], None] = None, force: bool = False) ‑> Optional[t9k.ah.core.Commit]
```

Commits changes to a branch of an Asset.

First delete, then add.

If no branch is provided, `:main` will be used.

For Windows platform, if you provide absolute paths for parameter `add`, change its format from 'C:\local\path' to '\C\local\path'.

## Examples

Add a file as object to specified branch of Model:
```python
ah.commit('model/llm/gpt2:v1', msg='add ...', add=['model.pt'])
```

Specify a path in Asset for a file to add:
```python
ah.commit('model/llm/gpt2:v1', msg='add ...', add={'model.pt': 'saved_model/'})
```

Add all files under a directory as objects (with the directory):
```python
ah.commit('model/llm/gpt2:v1', msg='add ...', add=['./saved_model'])
```

Add all files under a directory as objects (without the directory):
```python
ah.commit('model/llm/gpt2:v1', msg='add ...', add=['./saved_model/*'])
```

Specify a path in Asset for a directory to add:
```python
ah.commit('model/llm/gpt2:v1', msg='add ...', add={'./saved_model': 'path/to/[saved_model]'})
# or
ah.commit('model/llm/gpt2:v1', msg='add ...', add={'./saved_model': 'path/to/renamed_dir'})
```

Delete an object from a Dataset:
```python
ah.commit('dataset/images/cifar10', msg='delete ...', delete=['0.png'])
```

Delete all objects under the specified path:
```python
ah.commit('dataset/images/cifar10', msg='delete ...', delete=['data/'])
```

## Args

* **path** (*str*)

    Path of the branch.

* **msg** (*str*)

    Commit message.

* **delete** (*Optional[Sequence[str]]*)

    Files or directories to delete from the branch, can be a sequence of paths in branch or `None`. If empty sequence or `None`, delete nothing. If the files or directories to delete do not exist, do nothing (rather than raise an error). Here format `a/.../b` signifies a file, while `a/.../b/` signifies a directory.

* **add** (*Union[Sequence[str], Mapping[str, str], None]*)

    Files or directories to add to the branch, can be a sequence of local paths, a mapping from local paths to their paths in Asset, or `None`. If empty sequence, empty mapping or `None`, add nothing.

* **force** (*bool*)

    Whether to create a new commit if unknown changes or unimplemented changes are found.

## Returns

A `Commit` instance representing created commit if changes are
commited, `None` if not.
