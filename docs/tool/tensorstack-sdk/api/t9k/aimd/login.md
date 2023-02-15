---
title: t9k.aimd.login
---

# t9k.aimd.login

```python
login(host: Optional[str] = None, api_key: Optional[str] = None, timeout: Optional[int] = None, unable_to_connect_ok: bool = False) ‑> None
```

Logs in to AIMD server.

Sets up the client that corresponds with AIMD server.

## Args

* **host** (*Optional[str]*)

    URL of server. Defaults to server URL given by SDK config file if one is set.

* **api_key** (*Optional[str]*)

    API Key for requesting server. Defaults to API Key given by SDK config file if one is set.

* **timeout** (*Optional[int]*)

    How many seconds to wait for server to send data before giving up.

* **unable_to_connect_ok** (*bool*)

    If False and client is unable to connect to server, raise ConnectionError; if True and unable to connect, this setting up is invalid.

## Raises

* **requests.HTTPError**

    Unable to connect to server and `unable_to_connect_ok` is False.
