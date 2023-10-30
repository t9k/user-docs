---
title: t9k.ah.list
---

# t9k.ah.list

```python
list(path: str, resource: str = 'default') ‑> List[Dict[str, Any]]
```

Lists resources.

Based on the provided `path`, list Folders with the specified Asset kind, Assets within the specified Folder, or all objects of the specified reference (branch, tag or commit) of Asset.

To list Folders that are shared with you, set `path='shared/model'` (or `path='shared/dataset'`); to list Folders that are public, set `path='/public/t9k-assethub/model'` (or `path='/public/t9k-assethub/dataset'`).

To list branches, provide a `path` that points to an Asset and set `resource='branch'`; to list tags, provide a `path` that points to an Asset and set `resource='tag'`; to list commits, provide a `path` that points to a branch of an Asset and set `resource='commit'`.

If a reference is expected but omitted, `:main` will be used.

## Examples

List Model Folders that you own:
```python
folders = ah.list('model')
```

List Model Folders that are shared with you:
```python
folders = ah.list('shared/model')
```

List Model Folders that are public:
```python
folders = ah.list('/public/t9k-assethub/model')
```

List Models in your own Folder:
```python
models = ah.list('model/llm')
```

List Models in another user's Folder:
```python
models = ah.list('/user1/t9k-assethub/model/llm')
```

List objects of specified branch of Model:
```python
objects = ah.list('model/llm/gpt2:v1')
```

List objects of specified tag of Dataset:
```python
objects = ah.list('dataset/images/cifar10:20220101')
```

List branches of specified Model:
```python
branches = ah.list('model/llm/gpt2', resource='branch')
```

List tags of specified Model:
```python
tags = ah.list('model/llm/gpt2', resource='tag')
```

List commits of specified branch of Model:
```python
commits = ah.list('model/llm/gpt2:v1', resource='commit')
```

List commits of specified Dataset:
```python
commits = ah.list('dataset/images/cifar10', resource='commit')
```

## Args

* **path** (*str*)

    Path to be listed.

* **resource** (*str*)

    Kind of the resources, must be `'default'`, `'branch'`, '`tag`' or `'commit'`. This parameter is used to list branches, tags or commits: to list branches, provide a `path` that points to an Asset and set `resource='branch'`; to list tags, provide a `path` that points to an Asset and set `resource='tag'`; to list commits, provide a `path` that points to a branch of an Asset and set `resource='commit'`.

## Returns

A list of resources.
