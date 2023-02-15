---
title: t9k.aimd.trial.Trial
---

# t9k.aimd.trial.Trial

```python
Trial(trial_data: Dict[str, Any], local_name: Optional[str] = None)
```

Implementation of Trial, a run of a specific model for certain ML task.

You can save data of Trial to a local YAML file or load Trial from it.

## Args

* **trial_data** (*Dict[str, Any]*)

    Data of Trial to initialize a new Trial.

## Attributes

* **id** (*str*)

    ID of the Trial.

* **name** (*str*)

    Name of the Trial.

* **metrics** (*Dict[str, List[Dict[str, Dict[str, Union[str, int, float]]]]]*)

    Metrics produced in the Trial.

* **params** (*Any*)

    Hyperparameters of the Trial.

* **input_artifacts** (*List[str]*)

    Input Artifacts of the Trial.

* **output_artifacts** (*List[str]*)

    Output Artifacts of the Trial.

## Methods

### finish

```python
finish(*args, **kwargs)
```

### log

```python
log(self, metrics_type: str, metrics: Dict[str, float], step: int, epoch: Optional[int] = None, check_status: bool = True) ‑> None
```

Logs metrics of Trial.

#### Args

* **metrics_type** (*str*)

    Type of metrics, 'train' (or 'training'), 'val' (or 'validate', 'validation'), 'test' (or 'testing', 'eval', 'evaluate', 'evaluation') for training metrics, validation metrics, testing metrics respectively. Besides, you can also use other arbitrary string as custom type of metric.

* **metrics** (*Dict[str, float]*)

    Additional metrics to be logged.

* **step** (*int*)

    Number of step that metrics belong to.

* **epoch** (*Optional[int]*)

    Number of epoch that metrics belong to.

* **check_status** (*bool*)

    If True and current status of Trial is 'Initializing', update it to 'Running'.

### mark_input

```python
mark_input(self, artifact: t9k.aimd.artifact.Artifact) ‑> None
```

Adds ID of the Artifact to list of input Artifacts.

The Artifact must have `artifact._is_open == False`.

### mark_output

```python
mark_output(self, artifact: t9k.aimd.artifact.Artifact) ‑> None
```

Adds ID of the Artifact to list of output Artifacts.

The Artifact must have `artifact._can_be_logged == True`.

### parse_from_dict

```python
parse_from_dict(self, trial_data: Dict[str, Any]) ‑> None
```

Parses Trial instance from a dict.

### to_dict

```python
to_dict(self) ‑> Dict[str, Any]
```

Converts Trial instance to a dict and returns it.

### upload

```python
upload(self, folder_id: Optional[str] = None, folder_path: Optional[str] = None, make_folder: bool = None, conflict_strategy: Optional[str] = None) ‑> Optional[Dict[str, str]]
```

Uploads Trial to server.
