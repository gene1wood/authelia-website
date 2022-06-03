---
title: "authelia-scripts rsa generate"
description: "Reference for the authelia-scripts rsa generate command."
lead: ""
date: 2022-05-31T11:13:56+10:00
lastmod: 2022-06-02T23:28:13+10:00
draft: false
images: []
menu:
  reference:
    parent: "cli-authelia-scripts"
weight: 130
toc: true
---

## authelia-scripts rsa generate

Generate a RSA keypair

```
authelia-scripts rsa generate [flags]
```

### Options

```
  -d, --dir string     Target directory where the keypair will be stored
  -h, --help           help for generate
  -b, --key-size int   Sets the key size in bits (default 2048)
```

### Options inherited from parent commands

```
      --buildkite          Set CI flag for Buildkite
      --log-level string   Set the log level for the command (default "info")
```

### SEE ALSO

* [authelia-scripts rsa](authelia-scripts_rsa.md)	 - Commands related to rsa keypair generation

###### Auto generated by spf13/cobra on 2-Jun-2022