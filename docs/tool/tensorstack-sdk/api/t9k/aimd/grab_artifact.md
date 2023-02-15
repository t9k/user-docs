---
title: t9k.aimd.grab_artifact
---

# t9k.aimd.grab_artifact

```python
grab_artifact(artifact_path: Optional[str] = None, artifact_id: Optional[str] = None, artifact_ref: Optional[str] = None) ‑> t9k.aimd.artifact.Artifact
```

Grabs an Artifact from local path or server.

Priorities of the arguments: artifact_path > artifact_id > artifact_ref.

If `artifact_path` is provided, load from this local path.

If `artifact_id` is provided, this function will search `ARTIFACT_PATH` for sub-directory whose name matches `artifact_id`. If 1 match, load this Artifact; if no match and CLIENT is online, try to load the Artifact with this ID from server; else raise a RuntimeError.

If `artifact_ref` is provided, this function will send a request to server for ID of Artifact corresponding to the reference. The value of `artifact_ref` can be in one of the following forms:

* `<folder-id>/<repo-name>[:<tag>]`
* `<folder-path>/<repo-name>[:<tag>]`
* `<repo-id>[:<tag>]`

If `:<tag>` is not provided, default tag `:latest` will be used.

## Examples

```python
dateset_artifact = aimd.grab_artifact(
    artifact_id='5766682a-6528-4bff-8aae-7d80f3ff76f6')
dateset_artifact.download()
trial.mark_input(dateset_artifact)
```

## Args

* **artifact_path** (*Optional[str]*)

    Local path of the Artifact.

* **artifact_id** (*Optional[str]*)

    ID of the Artifact.

* **artifact_ref** (*Optional[str]*)

    Reference of the Artifact.

## Returns

An Artifact instance grabbed from local path or server.
