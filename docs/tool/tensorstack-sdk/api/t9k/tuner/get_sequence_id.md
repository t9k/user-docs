---
title: t9k.tuner.get_sequence_id
---

# t9k.tuner.get_sequence_id

```python
get_sequence_id()
```

Gets trial job sequence nubmer. A sequence number is an integer value assigned to each trial job base on the order they are submitted, incremental starting from 0. In one experiment, both trial job ID and sequence number are unique for each trial job, they are of different data types.

## Returns

Sequence number of current trial job which is calling this API.
