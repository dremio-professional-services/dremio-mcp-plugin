# Session engine and routing tag

Sources: [SET ENGINE](https://docs.dremio.com/dremio-cloud/sql/commands/set-engine/),
[RESET ENGINE](https://docs.dremio.com/dremio-cloud/sql/commands/reset-engine/),
[SET TAG](https://docs.dremio.com/dremio-cloud/sql/commands/set-tag/), and
[RESET TAG](https://docs.dremio.com/dremio-cloud/sql/commands/reset-tag/).

## Engine selection

```sql
SET ENGINE <engine_name>;
RESET ENGINE;
```

`SET ENGINE` selects the engine for subsequent statements in the current
session. It overrides Workload Management routing rules for that session; the
engine must be available and the user must have `USAGE`. `RESET ENGINE` removes
the session override so standard routing applies again. Neither setting persists
to a new session.

```sql
SET ENGINE analytics_engine;
SELECT CURRENT_ENGINE();
RESET ENGINE;
```

## Routing tag

```sql
SET TAG <tag_name>;
RESET TAG;
```

`SET TAG` supplies a session routing tag for Workload Management rules. It
overrides a pre-existing `ROUTING_TAG` connection property for the session;
`RESET TAG` removes the session-specific value. Define a matching routing rule
before relying on a tag for routing.

```sql
SET TAG dashboard;
RESET TAG;
```

`TAG` here is a session-routing label. This reference deliberately contains no
catalog branch, tag, or queue syntax.
