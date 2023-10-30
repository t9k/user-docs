---
title: t9k.em.login
---

# t9k.em.login

```python
login(ais_host: Optional[str] = None, api_key: Optional[str] = None, timeout: Optional[int] = None) ‑> None
```

Logs in to AIStore server.

Sets up the client that corresponds with AIStore server.

## Args

* **ais_host** (*Optional[str]*)

    URL of AIStore server. Defaults to `t9k.CONFIG['aistore_host']`.

* **api_key** (*Optional[str]*)

    API Key for requesting server. Defaults to `t9k.CONFIG['api_key']`.

* **timeout** (*Optional[int]*)

    How many seconds to wait for server to send data before giving up.

## Raises

* **requests.HTTPError**

    Unable to connect to the server and `unable_to_connect_ok` is False.
