---
title: t9k.ah.core.Folder
---

# t9k.ah.core.Folder

```python
Folder(path: str, id_: str, owner: str, asset_kind: str, name: str, labels: List[str], description: str, extra: str)
```

Represents a Asset Hub Folder in server.

## Attributes

* **path** (*str*)

    Path of the Folder.

* **id** (*str*)

    ID of the Folder in server.

* **owner** (*str*)

    Owner of the Folder.

* **kind** (*str*)

    Kind of the Folder, is a string `'Model'` or `'Dataset'`.

* **name** (*str*)

    Name of the Folder.

* **labels** (*List[str]*)

    Labels of the Folder.

* **description** (*str*)

    Description of the Folder.

* **extra** (*str*)

    Extra information about the Folder.

* **alive** (*bool*)

    Whether the Folder is alive.

## Methods

### create_asset

```python
create_asset(self, name: str, labels: Optional[Sequence[str]] = None, description: str = '', exist_ok: bool = False) ‑> Union[t9k.ah.core.Model, t9k.ah.core.Dataset]
```

Creates an Asset in this Folder.

#### Args

* **name** (*str*)

    Name of the Asset.

* **labels** (*Optional[Sequence[str]]*)

    Labels of the Asset.

* **description** (*str*)

    Description of the Asset.

* **exist_ok** (*bool*)

    If True and Asset with `name` already exists, return a `Model` or `Dataset` instance representing this Asset; if False and Asset exists, raise a `RuntimeError`.

#### Returns

A `Model` or `Dataset` instance representing created Model or
Dataset, depending on Asset kind of this Folder.

### delete

```python
delete(self) ‑> None
```

Deletes this Folder.

### get_asset

```python
get_asset(self, name: str) ‑> Union[t9k.ah.core.Model, t9k.ah.core.Dataset]
```

Gets an Asset in this Folder.

If you want to get Asset directly by its path, use `ah.get_asset()`.

#### Args

* **name** (*str*)

    Name of the Asset.

#### Returns

A `Model` or `Dataset` instance representing retrieved Model or
Dataset, depending on Asset kind of this Folder.

### list_asset

```python
list_asset(self) ‑> List[Dict[str, Any]]
```

Lists Assets in this Folder.

### update

```python
update(self, name: Optional[str] = None, labels: Optional[Sequence[str]] = None, description: Optional[str] = None) ‑> None
```

Updates the metadata of this Folder.

If none of the args is provided, do nothing.

#### Args

* **name** (*Optional[str]*)

    New name of this Folder.

* **labels** (*Optional[Sequence[str]]*)

    New labels of this Folder.

* **description** (*Optional[str]*)

    New description of this Folder.
