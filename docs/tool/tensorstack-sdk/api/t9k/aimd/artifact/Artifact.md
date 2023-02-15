---
title: t9k.aimd.artifact.Artifact
---

# t9k.aimd.artifact.Artifact

```python
Artifact(artifact_data: Dict[str, Any], repo_data: Dict[str, str], object_data: Optional[Sequence[Dict[str, Any]]] = None, can_be_logged: bool = True)
```

Implementation of Artifact, a set of files that a Trial inputs or outputs.

## Args

* **artifact_data** (*Dict[str, Any]*)

    Data of Artifact to initialize a new Artifact.

* **repo_data** (*Dict[str, str]*)

    Data of the repo that the Artifact belongs to.

* **object_data** (*Optional[Sequence[Dict[str, Any]]]*)

    Data of objects of the Artifact.

* **can_be_logged** (*bool*)

    If True, the Artifact initialized can be logged by a Trial.

## Attributes

* **id** (*str*)

    ID of the Artifact.

* **name** (*str*)

    Name of repo of the Artifact.

* **description** (*str*)

    Description of the Artifact.

* **commit** (*str*)

    Hash of commit of the Artifact. It is None if the Artifact has never been uploaded.

* **version** (*str*)

    Version of the Artifact. It is None if the Artifact has never been uploaded.

* **aliases** (*List[str]*)

    Aliases of the Artifact.

* **objects** (*List[Dict[str, str]]*)

    Data of objects of the Artifact.

* **repo** (*Dict[str, str]*)

    Data of repo of the Artifact.

* **remote** (*List[Dict[str, str]]*)

    Location of the Artifact in remote AIMD server. It is None if the Artifact has never been uploaded.

* **is_open** (*bool*)

    If True, the Artifact has not been uploaded yet and thus open to changes.

## Methods

### add_dir

```python
add_dir(self, *args, **kwargs)
```

### add_file

```python
add_file(self, *args, **kwargs)
```

### add_reference

```python
add_reference(self, *args, **kwargs)
```

### download

```python
download(self) ‑> None
```

Downloads all Artifact objects to local.

For each object, if it already exists in object path and passes size
and MD5 checking, it will not be downloaded.

### local_path

```python
local_path(self, key: Optional[str] = None) ‑> Optional[str]
```

Returns local path of the Artifact of its object.

### parse_from_dict

```python
parse_from_dict(self, artifact_data: Dict[str, Any]) ‑> None
```

Parses an Artifact instance from a dict.

### to_dict

```python
to_dict(self) ‑> Dict[str, Any]
```

Converts Artifact instance to a dict and returns it.

### upload

```python
upload(self, folder_id: Optional[str] = None, folder_path: Optional[str] = None, make_folder: bool = False) ‑> Dict[str, Any]
```

Uploads Artifact to server.

For information of the arguments, refer to `create_trial()` API.

#### Returns

Data of the posted Artifact from server.
