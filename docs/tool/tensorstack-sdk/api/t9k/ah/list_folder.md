---
title: t9k.ah.list_folder
---

# t9k.ah.list_folder

```python
list_folder(type_: str = 'all', scope: str = 'all') ‑> List[Dict[str, Any]]
```

Lists Folders.

## Examples

List all Folders:
```python
ah.list_folder()
```

List all Model Folders that current user owns:
```python
ah.list_folder(type_='model', scope='own')
```

## Args

* **type_** (*str*)

    Type of the Folders, must be `'model'`, `'dataset'` or `all`. If `all`, both Model and Dataset Folders are listed.

* **scope** (*str*)

    Scope of listing, must be `'own'`, `'shared'`, `'public'` or `'all'`.

## Returns

Folders' data retrieved.
