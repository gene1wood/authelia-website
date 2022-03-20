---
title: "Common"
description: "Common configuration options and notations."
lead: "An introduction into configuring Authelia."
date: 2022-03-19T04:53:05+00:00
lastmod: 2022-03-19T04:53:05+00:00
draft: false
images: []
menu:
  configuration:
    parent: "prologue"
weight: 100200
toc: true
---

## Duration Notation Format

We have implemented a string/integer based notation for configuration options that take a duration of time. This section
describes the implementation of this. You can use this implementation in various areas of configuration such as:

- session:
  - expiration
  - inactivity
  - remember_me_duration
- regulation:
  - ban_time
  - find_time
- ntp:
  - max_desync
- webauthn:
  - timeout

The way this format works is you can either configure an integer or a string in the specific configuration areas. If you
supply an integer, it is considered a representation of seconds. If you supply a string, it parses the string in blocks
of quantities and units (number followed by a unit letter).  For example `5h` indicates a quantity of 5 units of `h`.

While you can use multiple of these blocks in combination, ee suggest keeping it simple and use a single value.

### Unit Legend

|  Unit   | Associated Letter |
|:-------:|:-----------------:|
|  Years  |         y         |
| Months  |         M         |
|  Weeks  |         w         |
|  Days   |         d         |
|  Hours  |         h         |
| Minutes |         m         |
| Seconds |         s         |

### Examples

|     Desired Value     |        Configuration Examples         |
|:---------------------:|:-------------------------------------:|
| 1 hour and 30 minutes | `90m` or `1h30m` or `5400` or `5400s` |
|         1 day         | `1d` or `24h` or `86400` or `86400s`  |
|       10 hours        | `10h` or `600m` or `9h60m` or `36000` |

## TLS Configuration

Various sections of the configuration use a uniform configuration section called TLS. Notably LDAP and SMTP.
This section documents the usage.

### server_name

{{< confkey type="string" required="no" >}}

The key `server_name` overrides the name checked against the certificate in the verification process. Useful if you
require to use a direct IP address for the address of the backend service but want to verify a specific SNI.

### skip_verify

{{< confkey type="boolean" default="false" required="no" >}}

The key `skip_verify` completely negates validating the certificate of the backend service. This is not recommended,
instead you should tweak the `server_name` option, and the global option
[certificates directory](../miscellaneous/introduction.md#certificates_directory).

### minimum_version

{{< confkey type="string" default="TLS1.2" required="no" >}}

The key `minimum_version` controls the minimum TLS version Authelia will use when opening TLS connections.
The possible values are `TLS1.3`, `TLS1.2`, `TLS1.1`, `TLS1.0`. Anything other than `TLS1.3` or `TLS1.2`
are very old and deprecated. You should avoid using these and upgrade your backend service instead of decreasing
this value.