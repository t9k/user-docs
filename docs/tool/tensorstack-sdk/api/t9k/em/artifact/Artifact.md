---
title: t9k.em.artifact.Artifact
---

# t9k.em.artifact.Artifact

```python
Artifact(metadata: Dict[str, Any], objects: Optional[Dict[str, Dict[str, Any]]] = None)
```

Implementation of Artifact, a set of files that a Run inputs or outputs.

## Args

* **metadata** (*Dict[str, Any]*)

    Metadata to initialize a new Artifact.

* **objects** (*Optional[Dict[str, Dict[str, Any]]]*)

    Data of objects of the Artifact.

## Attributes

* **name** (*str*)

    Name of the Artifact.

* **labels** (*List[str]*)

    Labels of the Artifact.

* **description** (*str*)

    Description of the Artifact.

* **created_timestamp** (*str*)

    Created timestamp of the Artifact.

* **alternative_name** (*str*)

    Alternative name of the Artifact.

* **objects** (*List[Dict[str, str]]*)

    Data of objects of the Artifact.

* **remote** (*List[Dict[str, str]]*)

    Upload and download history of the Artifact.

* **local** (*str*)

    Local directory of the Artifact.

## Methods

### add_dir

```python
add_dir(self, dir_path: str, obj_path: Optional[str] = None) ‑> None
```

Adds all files under a local directory as objects of the Artifact.

The directory will be copied to local directory of the Artifact, the
specific subpath depends on its obj_path, for example:

```
# dir copied to `<local-dir>/a`
artifact.add_dir(dir_path='a/')
# or
artifact.add_dir(dir_path='a')
# or
artifact.add_dir(dir_path='a/', obj_path='a')

# dir copied to `<local-dir>/b/a`
artifact.add_dir(dir_path='a/', obj_path='b/')
# or
artifact.add_dir(dir_path='a/', obj_path='b/a')
```

### add_file

```python
add_file(self, file_path: str, obj_path: Optional[str] = None) ‑> None
```

Adds a local file as an object of the Artifact.

The file will be copied to local directory of the Artifact, the
specific subpath depends on its object path, for example:

```
# file copied to `<local-dir>/1.png`
artifact.add_file(file_path='1.png')
# or
artifact.add_file(file_path='1.png', obj_path='1.png')

# file copied to `<local-dir>/a/1.png`
artifact.add_file(file_path='1.png', obj_path='a/')
# or
artifact.add_file(file_path='1.png', obj_path='a/1.png')
```

### add_reference

```python
add_reference(self, uri: str, obj_path: Optional[str] = None) ‑> None
```

Adds a URI as an object reference to the Artifact.

### parse_from_dict

```python
parse_from_dict(self, data: Dict[str, Any]) ‑> None
```

Parses an Artifact instance from a dict.

### to_dict

```python
to_dict(self) ‑> Dict[str, Any]
```

Converts Artifact instance to a dict and returns it.

### upload

```python
upload(self, folder: str = 'default', make_folder: bool = False, conflict_strategy: str = 'new') ‑> None
```

Uploads this Artifact to server.

#### Args

* **folder** (*str*)

    Path of the Folder to which the Artifact is uploaded. If the provided path does not start with '/', `/<current-user>/` is prepended to it.

* **make_folder** (*bool*)

    If True and Folder with path `folder` does not exist, make the Folder and parent Folders as needed.

* **conflict_strategy** (*str*)

    Strategy adopted when an Artifact with the same name as the Artifact to be uploaded already exists in the Folder, must be 'skip', 'error', 'new' or 'replace'. If 'skip', skip the upload; if 'error', error out; if 'new', upload with the alternative name of Artifact; if 'replace', delete the existing Artifact and upload.
