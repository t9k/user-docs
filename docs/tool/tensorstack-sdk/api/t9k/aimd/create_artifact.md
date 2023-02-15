---
title: t9k.aimd.create_artifact
---

# t9k.aimd.create_artifact

```python
create_artifact(artifact_name: str, artifact_type: str, description: str = '', aliases: Union[str, Sequence[str], None] = None) ‑> t9k.aimd.artifact.Artifact
```

Creates and initializes a new artifact.

## Examples

```python
dateset_artifact = aimd.create_artifact(artifact_name='mnist',
                                        artifact_type='dataset')
```

## Args

* **artifact_name** (*str*)

    Name of the Artifact.

* **artifact_type** (*str*)

    Type of the Artifact.

* **description** (*str*)

    Description of the Artifact.

* **aliases** (*Union[str, Sequence[str], None]*)

    Aliase(s) of the Artifact. Can be a string or sequence of string or `None`.

## Returns

An Artifact instance created and initialized.
