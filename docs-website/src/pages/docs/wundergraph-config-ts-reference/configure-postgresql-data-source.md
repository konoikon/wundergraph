---
title: Configure PostgreSQL Data Source
pageTitle: WunderGraph - Configure PostgreSQL Data Source
description:
---

The PostgreSQL data source introspects the database and generates a GraphQL schema.

## Example Configuration

```typescript
// wundergraph.config.ts

const db = introspect.postgresql({
  apiNamespace: 'wundergraph',
  databaseURL: 'postgres://postgres:postgres@localhost:5432/wundergraph',
  introspection: {
    pollingIntervalSeconds: 5,
  },
})

const myApplication = new Application({
  name: 'app',
  apis: [db],
})
```

Define the `databaseURL` which is the connection string to the database.
To avoid naming conflicts, you should also define an `apiNamespace`.

The introspection result will be cached in the local file-system to make the development process faster.
Otherwise, WunderGraph would introspect the database every time you change an operation.

If you're planning to frequently change the database schema,
e.g. during development,
you should specify the `pollingIntervalSeconds` to 5 seconds for example.
This will make WunderGraph introspect the database every 5 seconds.
If the generated schema is changed, the file-system cache will be updated.
