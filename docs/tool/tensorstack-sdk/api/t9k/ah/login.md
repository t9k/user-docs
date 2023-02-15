---
title: t9k.ah.login
---

# t9k.ah.login

```python
login(host: Optional[str] = None, api_key: Optional[str] = None, timeout: Optional[int] = None) ‑> None
```

Logs in to Asset Hub server.

Sets up the client that corresponds with Asset Hub server.

## Args

* **host** (*Optional[str]*)

    URL of Asset Hub server. Defaults to server URL given by SDK config file if one is set.

* **api_key** (*Optional[str]*)

    API Key for requesting server. Defaults to API Key given by SDK config file if one is set.

* **timeout** (*Optional[int]*)

    How many seconds to wait for server to send data before giving up.

## Raises

* **requests.HTTPError**

    Unable to connect to server.
