---
title: "First Factor"
description: "Configuring Duo"
lead: "Authelia has multiple first factor methods. This section describes configuring this."
date: 2022-03-19T04:53:05+00:00
lastmod: 2022-03-19T04:53:05+00:00
draft: false
images: []
menu:
  configuration:
    parent: "first-factor"
weight: 102300
toc: true
---

There are two ways to store the users along with their password:

* LDAP: users are stored in remote servers like OpenLDAP, OpenAM or Microsoft Active Directory.
* File: users are stored in YAML file with a hashed version of their password.

## Configuration

```yaml
authentication_backend:
  disable_reset_password: false
  file: {}
  ldap: {}
```

## Options

### disable_reset_password

{{< confkey type="boolean" default="false" required="no" >}}

This setting controls if users can reset their password from the web frontend or not.

### file

The [file](file.md) authentication provider.

### ldap

The [LDAP](ldap.md) authentication provider.