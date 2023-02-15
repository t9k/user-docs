---
title: t9k.ah.create_folder
---

# t9k.ah.create_folder

```python
create_folder(type_: str, name: str, labels: Union[str, Sequence[str], None] = None, exist_ok: bool = False) ‑> t9k.ah.core.Folder
```

Creates a Folder.

## Examples

Create a Model Folder without labels:
```python
folder = ah.create_folder(type_='model', name='mnist-keras')
```

Create a Model Folder with three labels:
```python
folder = ah.create_folder(
    type_='model',
    name='mnist-keras',
    labels=['Image Classification', 'MNIST', 'Keras'])
```

## Args

* **type_** (*str*)

    Type of the Folder, must be `'model'` or `'dataset'`.

* **name** (*str*)

    Name of the Folder.

* **labels** (*Union[str, Sequence[str], None]*)

    Labels of the Folder, can be a string, a sequence of string or `None`.

* **exist_ok** (*bool*)

    If True and Folder with `type_` and `name` already exists, return a `Folder` instance representing this Folder; if False and Folder exists, raise a `RuntimeError`.

## Returns

A `Folder` instance representing created Folder.
