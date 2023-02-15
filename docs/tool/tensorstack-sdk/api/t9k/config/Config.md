---
title: t9k.config.Config
---

# t9k.config.Config

```python
Config()
```

SDK config.

## Static methods

### make_config_file

```python
make_config_file()
```

Makes a default SDK config file.

## Methods

### get

```python
get(self, key: str, default: Any = None) ‑> Any
```

### items

```python
items(self) ‑> ItemsView[str, Any]
```

### load

```python
load(self) ‑> None
```

Loads from SDK config file.

If SDK config file does not exist, make a default one.

### save

```python
save(self) ‑> None
```

Saves to SDK config file.

### to_dict

```python
to_dict(self) ‑> Dict[str, Any]
```

### update

```python
update(self, new_config: Dict[str, Any]) ‑> None
```
