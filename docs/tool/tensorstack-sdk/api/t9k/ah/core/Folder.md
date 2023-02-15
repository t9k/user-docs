---
title: t9k.ah.core.Folder
---

# t9k.ah.core.Folder

```python
Folder(id_: str, owner: str, type_: str, name: str, labels: Union[str, Sequence[str], None] = None)
```

Represents a Folder in server.

## Attributes

* **id** (*str*)

    ID of the Folder in server.

* **owner** (*str*)

    Owner of the Folder.

* **type** (*str*)

    Type of the Folder, is a string "model" or "dataset".

* **name** (*str*)

    Name of the Folder.

* **labels** (*List[str]*)

    Labels of the Folder.

## Methods

### create_asset

```python
create_asset(self, *args, **kwargs)
```

### delete

```python
delete(self, *args, **kwargs)
```

### get_asset

```python
get_asset(self, *args, **kwargs)
```

### list_asset

```python
list_asset(self, *args, **kwargs)
```

### update

```python
update(self, *args, **kwargs)
```
