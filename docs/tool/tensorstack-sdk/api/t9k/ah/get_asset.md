---
title: t9k.ah.get_asset
---

# t9k.ah.get_asset

```python
get_asset(id_: str) ‑> Union[t9k.ah.core.Model, t9k.ah.core.Dataset]
```

Gets an Asset directly by ID.

If you want to get Asset by its ref, use `ah.get_folder().get_asset()`.

## Args

* **id_** (*str*)

    ID of the Asset.

## Returns

A `Model` or `Dataset` instance representing retrieved Model or
Dataset.
