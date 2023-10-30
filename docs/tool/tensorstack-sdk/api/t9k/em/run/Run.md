---
title: t9k.em.run.Run
---

# t9k.em.run.Run

```python
Run(metadata: Dict[str, Any], hparams: Optional[Dict[str, Any]] = None, metrics: Optional[Dict[str, List[Dict[str, Dict[str, Union[str, int, float]]]]]] = None, platform: Optional[Dict[str, Any]] = None, git: Optional[Dict[str, Any]] = None)
```

Implementation of Run, a run of a specific model for certain ML task.

## Args

* **metadata** (*Dict[str, Any]*)

    Metadata to initialize a new Run.

* **hparams** (*Optional[Dict[str, Any]]*)

    Hyperparameters of the Run.

* **metrics** (*Optional[Dict[str, List[Dict[str, Dict[str, Union[str, int, float]]]]]]*)

    Metrics of the Run.

* **platform** (*Optional[Dict[str, Any]]*)

    Platform information of the Run.

* **git** (*Optional[Dict[str, Any]]*)

    Git information of the Run.

## Attributes

* **name** (*str*)

    Name of the Run.

* **labels** (*List[str]*)

    Labels of the Run.

* **description** (*str*)

    Description of the Run.

* **start_timestamp** (*str*)

    Start timestamp of the Run.

* **end_timestamp** (*str*)

    End timestamp of the Run.

* **status** (*str*)

    Status of the Run.

* **alternative_name** (*str*)

    Alternative name of the Run.

* **associations** (*Dict[str, List[Dict[str, str]]]*)

    Input and output resources of the Run.

* **hparams** (*Any*)

    Hyperparameters of the Run.

* **metrics** (*Dict[str, List[Dict[str, Dict[str, Union[str, int, float]]]]]*)

    Metrics produced in the Run.

* **platform** (*Dict[str, Any]*)

    Platform information of the Run.

* **git** (*Dict[str, Any]*)

    Git information of the Run.

* **remote** (*List[Dict[str, str]]*)

    Upload and download history of the Run.

* **local** (*str*)

    Local directory of the Run.

## Methods

### finish

```python
finish(*args, **kwargs)
```

### log

```python
log(self, type: str, metrics: Dict[str, float], step: int, epoch: Optional[int] = None) ‑> None
```

Logs a set of metrics of Run.

#### Args

* **type** (*str*)

    Type of the metrics, 'train' (or 'training'), 'val' (or 'validate', 'validation') and 'test' (or 'testing', 'eval', 'evaluate', 'evaluation') for training, validation and testing metrics respectively. Besides, you can also use other arbitrary string as custom type of the metrics.

* **metrics** (*Dict[str, float]*)

    Additional metrics to be logged.

* **step** (*int*)

    Number of the step that the metrics belong to.

* **epoch** (*Optional[int]*)

    Number of the epoch that the metrics belong to.

### mark_input

```python
mark_input(self, resource: Union[t9k.em.artifact.Artifact, t9k.ah.core.Model, t9k.ah.core.Dataset, t9k.ah.core.Branch, t9k.ah.core.Tag, t9k.ah.core.Commit]) ‑> None
```

Marks an Artifact, Model or Dataset as an input of this Run.

### mark_output

```python
mark_output(self, resource: Union[t9k.em.artifact.Artifact, t9k.ah.core.Model, t9k.ah.core.Dataset, t9k.ah.core.Branch, t9k.ah.core.Tag, t9k.ah.core.Commit]) ‑> None
```

Marks an Artifact, Model or Dataset as an output of this Run.

### parse_from_dict

```python
parse_from_dict(self, data: Dict[str, Any]) ‑> None
```

Parses a Run instance from a dict.

### to_dict

```python
to_dict(self) ‑> Dict[str, Any]
```

Converts Run instance to a dict and returns it.

### upload

```python
upload(self, folder: str = 'default', make_folder: bool = False, conflict_strategy: str = 'new') ‑> None
```

Uploads this Run to server.

If this Run has input or output Artifacts, these Artifacts are uploaded
as well if they have not been uploaded, and these associations are
uploaded.

#### Args

* **folder** (*str*)

    Path of the Folder to which the Run is uploaded. If the provided path does not start with '/', `/<current-user>/` is prepended to it.

* **make_folder** (*bool*)

    If True and Folder with path `folder` does not exist, make the Folder and parent Folders as needed.

* **conflict_strategy** (*str*)

    Strategy adopted when a Run with the same name as the Run to be uploaded already exists in the Folder, must be 'skip', 'error', 'new' or 'replace'. If 'skip', skip the upload; if 'error', error out; if 'new', upload with the alternative name of Run; if 'replace', delete the existing Run and upload.
