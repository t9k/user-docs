---
title: t9k.ah.core.Dataset
---

# t9k.ah.core.Dataset

```python
Dataset(id_: str, folder: Folder, name: str, labels: Union[str, Sequence[str], None] = None)
```

Represents a Dataset in server.

## Attributes

## Ancestors

* `t9k.ah.core._Asset`
* **id** (*Any*)

    ID of the Dataset in server.

* **folder** (*Any*)

    A Folder instance corresponding to the Folder that the Dataset belongs to.

* **type** (*Any*)

    A string "dataset".

* **name** (*Any*)

    Name of the Dataset.

* **labels** (*Any*)

    Labels of the Dataset.

* **commit_id** (*str*)

    ID of the commit that the main branch points to.

## Methods

### create_commit

```python
create_commit(self, *args, **kwargs)
```

### download

```python
download(self, *args, **kwargs)
```

### get_commit

```python
get_commit(self, *args, **kwargs)
```

### get_tag

```python
get_tag(self, *args, **kwargs)
```

### list_commit

```python
list_commit(self, *args, **kwargs)
```

### list_object

```python
list_object(self, *args, **kwargs)
```

### list_tag

```python
list_tag(self, *args, **kwargs)
```
