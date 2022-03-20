---
title: "SQLite3"
description: "SQLite3 Configuration"
lead: "The SQLite3 storage provider."
date: 2022-03-19T04:53:05+00:00
lastmod: 2022-03-19T04:53:05+00:00
draft: false
images: []
menu:
  configuration:
    parent: "storage"
weight: 107500
toc: true
---

If you don't have a SQL server, you can use [SQLite](https://en.wikipedia.org/wiki/SQLite).
However please note that this setup will prevent you from running multiple
instances of Authelia since the database will be a local file.

Use of this storage provider leaves Authelia [stateful](../../features/statelessness.md). It's important in highly
available scenarios to use one of the other providers, and we highly recommend it in production environments, but this
requires you setup an external database.

## Configuration

```yaml
storage:
  encryption_key: a_very_important_secret
  local:
    path: /config/db.sqlite3
```

## Options

### encryption_key
See the [encryption_key docs](./index.md#encryption_key).

### path

{{< confkey type="string" required="yes" >}}

The path where the SQLite3 database file will be stored. It will be created if the file does not exist.