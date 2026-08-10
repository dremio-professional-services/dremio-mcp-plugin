# Session queue and tag routing

Current Enterprise syntax:

- https://docs.dremio.com/current/reference/sql/commands/set-queue/
- https://docs.dremio.com/current/reference/sql/commands/reset-queue/
- https://docs.dremio.com/current/reference/sql/commands/set-tag/
- https://docs.dremio.com/current/reference/sql/commands/reset-tag/

```sql
SET QUEUE <queue_name>;
RESET QUEUE;
SET TAG <tag_name>;
RESET TAG;
```

`SET QUEUE` specifies the queue for subsequent queries in the current session;
`RESET QUEUE` returns queue routing to the default WLM rules. `SET TAG` sets a
session routing tag; `RESET TAG` clears it and returns routing to default WLM
rules unless another explicit session setting applies. Names must refer to
configured WLM objects/rules.

This is Enterprise queue/tag routing only. Do not use or suggest `SET ENGINE`
in this skill.
