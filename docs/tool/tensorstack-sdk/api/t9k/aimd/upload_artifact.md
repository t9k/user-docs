---
title: t9k.aimd.upload_artifact
---

# t9k.aimd.upload_artifact

```python
upload_artifact(artifact_path: Union[str, Sequence[str], None] = None, artifact_id: Union[str, Sequence[str], None] = None, repo_path: Optional[str] = None, repo_name: Optional[str] = None, folder_id: Optional[str] = None, folder_path: Optional[str] = None, make_folder: bool = False) ‑> None
```

Uploads one or multiple Artifacts that are saved locally.

## Examples

Upload one Artifact by its path:
```python
aimd.upload_artifact(artifact_path='.aimd/artifacts/mnist_keras_model/'
            '18c77b08-d3f4-4a88-a0e3-9f578c7f6750')
# or
aimd.upload_artifact(artifact_path='/path/to/workspace/.aimd/artifacts'
            '/mnist_keras_model/18c77b08-d3f4-4a88-a0e3-9f578c7f6750')
```

Upload one Artifact by its ID:
```python
aimd.upload_artifact(artifact_id='18c77b08-d3f4-4a88-a0e3-9f578c7f6750')
```

Upload multiple Artifacts by their IDs:
```python
aimd.upload_artifact(artifact_id=['18c77b08-d3f4-4a88-a0e3-9f578c7f6750',
                        '6feee8d9-03bf-49bb-9812-b47d3cce4e05'])
```

Upload all Artifacts in a repo:
```python
aimd.upload_artifact(repo_path='.aimd/artifacts/mnist_keras_model/')
# or
aimd.upload_artifact(repo_name='mnist_keras_model')
```

## Args

* **artifact_path** (*Union[str, Sequence[str], None]*)

    Local path of the Artifact to be uploaded, can be a path of one Artifact or a list of paths of multiple Artifacts.

* **artifact_id** (*Union[str, Sequence[str], None]*)

    ID of the Artifact to be uploaded, can be an ID of one Artifact or a list of IDs of multiple Artifacts. This function will search `ARTIFACT_PATH` for sub-directory whose name matches `artifact_id`.

* **repo_path** (*Optional[str]*)

    Local path of the Artifact repo in which all Artifacts are to be uploaded.

* **repo_name** (*Optional[str]*)

    Name of the Artifact repo in which all Artifacts are to be uploaded. This function will search `ARTIFACT_PATH` for sub-directory whose name matches `repo_name`.

* **folder_id** (*Optional[str]*)

    ID of the folder to which the Artifact is uploaded.

* **folder_path** (*Optional[str]*)

    Path of the folder to which the Artifact is uploaded. If `folder_id` is provided, `folder_path` will not be used; if neither `folder_id` or `folder_path` is provided, the Artifact will be uploaded to folder with path `/default`.

* **make_folder** (*bool*)

    If True and folder with `folder_path` does not exist, make the folder and parent folders as needed.
