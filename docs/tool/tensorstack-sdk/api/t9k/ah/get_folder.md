---
title: t9k.ah.get_folder
---

# t9k.ah.get_folder

```python
get_folder(owner: Optional[str] = None, type_: Optional[str] = None, name: Optional[str] = None, id_: Optional[str] = None) ‑> t9k.ah.core.Folder
```

Gets a Folder.

## Examples

Get a Folder of current user:
```python
folder = ah.get_folder(type_='model', name='mnist-keras')
```

Get a Folder of another user:
```python
folder = ah.get_folder(owner='another',
                       type_='model',
                       name='mnist-keras')
```

Get a Folder by ID:
```python
folder = ah.get_folder(id_='b81f187a-ad73-4f6e-b3b4-8b95b063ec32')
```

## Args

* **owner** (*Optional[str]*)

    Owner of the Folder. Default to current user that logged in to Asset Hub server, which means you get your own Folder. You can also specify another user, which means you get another user's Folder. In the second case, you (current user) must have view permission of the Folder.

* **type_** (*Optional[str]*)

    Type of the Folder.

* **name** (*Optional[str]*)

    Name of the Folder.

* **id_** (*Optional[str]*)

    ID of the Folder. If this arg is provided, all of the above args are not required.

## Returns

A `Folder` instance representing retrieved Folder.
