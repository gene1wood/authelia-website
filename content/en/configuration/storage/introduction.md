---
title: "Storage"
description: "Storage Configuration"
lead: "An introduction into configuring Authelia."
date: 2022-03-19T04:53:05+00:00
lastmod: 2022-03-19T04:53:05+00:00
draft: false
images: []
menu:
  configuration:
    parent: "storage"
weight: 107100
toc: true
---

**Authelia** supports multiple storage backends. The backend is used to store user preferences, 2FA device handles and
secrets, authentication logs, etc...

The available storage backends are listed in the table of contents below.

## Configuration

```yaml
storage:
  encryption_key: a_very_important_secret
  local: {}
  mysql: {}
  postgres: {}
```

## Options

### encryption_key

{{< confkey type="string" required="yes" >}}

The encryption key used to encrypt data in the database. We encrypt data by creating a sha256 checksum of the provided
value, and use that to encrypt the data with the AES-GCM 256bit algorithm.

The minimum length of this key is 20 characters, however we generally recommend above 64 characters.

See [securty measures](../../security/measures.md#storage-security-measures) for more information.

### local

See [SQLite](sqlite.md).

### mysql

See [MySQL](mysql.md).

### postgres

See [PostgreSQL](postgres.md).