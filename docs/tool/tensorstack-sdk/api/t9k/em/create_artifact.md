---
title: t9k.em.create_artifact
---

# t9k.em.create_artifact

```python
create_artifact(name: str, labels: Optional[Sequence[str]] = None, description: str = '') ‑> t9k.em.artifact.Artifact
```

Creates and initializes a new Artifact.

The local files of Artifact are placed under the parent directory specified by the environment variable `EM_ARTIFACT_PARENT_DIR` (default is relative path `.em/artifacts`).

## Examples

```python
tensorboard_artifact = em.create_artifact(name='tensorboard_logs')
```

## Args

* **name** (*str*)

    Name of the Artifact.

* **labels** (*Optional[Sequence[str]]*)

    Labels of the Artifact.

* **description** (*str*)

    Description of the Artifact.

## Returns

An Artifact instance created and initialized.
