---
title: t9k.ah.login
---

# t9k.ah.login

```python
login(ah_host: Optional[str] = None, ais_host: Optional[str] = None, api_key: Optional[str] = None, timeout: Optional[int] = None) ‑> None
```

Logs in to AIStore server and Asset Hub server.

Sets up the client that corresponds with AIStore server and Asset Hub server.

## Args

* **ah_host** (*Optional[str]*)

    URL of Asset Hub server. Defaults to `t9k.CONFIG['asset_hub_host']`.

* **ais_host** (*Optional[str]*)

    URL of AIStore server. Defaults to `t9k.CONFIG['aistore_host']`.

* **api_key** (*Optional[str]*)

    API Key for requesting server. Defaults to `t9k.CONFIG['api_key']`.

* **timeout** (*Optional[int]*)

    How many seconds to wait for server to send data before giving up.

## Raises

* **requests.HTTPError**

    Unable to connect to the server.
