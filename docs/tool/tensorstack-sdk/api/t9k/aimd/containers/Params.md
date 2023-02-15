---
title: t9k.aimd.containers.Params
---

# t9k.aimd.containers.Params

```python
Params(upload: Callable, init_params: Dict[str, Union[str, int, float, bool, None, List[~T], Tuple[], Dict[~KT, ~VT]]] = None)
```

Container class to hold hyperparameters of Trial.

It is recommended to set all hyperparameters by calling `update` method once before building the model. Nevertheless, you are free to operate hyperparameters like items of a dict or attributes of an object.

## Examples

Recommended method of setting hyperparameters:
```python
trial.update({
    'batch_size': 32,
    'epochs': 10,
})
```

Assign parameter like an item of dict or attribute of object:
```python
trial.params['batch_size'] = 32
trial.params.epochs = 10
```

## Args

* **upload** (*Callable*)

    Function that is called to upload hyperparameters every time hyperparameters are updated.

* **init_params** (*Dict[str, Union[str, int, float, bool, None, List[~T], Tuple[], Dict[~KT, ~VT]]]*)

    Initial hyperparameters.

## Ancestors

* `collections.abc.MutableMapping`

## Methods

### as_dict

```python
as_dict(self)
```

### items

```python
items(self)
```

D.items() -> a set-like object providing a view on D's items

### keys

```python
keys(self)
```

D.keys() -> a set-like object providing a view on D's keys

### parse

```python
parse(self, dist_tf_strategy=None, dist_torch_model=None, dist_hvd=None)
```

Parses hyperparameters from various objects of various frameworks.

#### Args

* **dist_tf_strategy**

    TensorFlow distribution strategy instance if `tf.distribute` is used for distributed training.

* **dist_torch_model**

    PyTorch model wrapped with DP or DDP if `torch.distributed` is used for distributed training.

* **dist_hvd**

    Used module such as `horovod.keras` and `horovod.torch` if Horovod is used for distributed training.

### update

```python
update(self, new_params: Dict[str, Any], override: bool = True)
```

Updates with new params.

#### Args

* **new_params** (*Dict[str, Any]*)

    New params to be updated with.

* **override** (*bool*)

    Whether to override current params.

### values

```python
values(self)
```

D.values() -> an object providing a view on D's values
