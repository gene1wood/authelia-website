---
title: "authelia access-control check-policy"
description: "Reference for the authelia access-control check-policy command."
lead: ""
date: 2022-05-31T11:13:56+10:00
lastmod: 2022-06-02T23:28:13+10:00
draft: false
images: []
menu:
  reference:
    parent: "cli-authelia"
weight: 130
toc: true
---

## authelia access-control check-policy

Checks a request against the access control rules to determine what policy would be applied

### Synopsis


Checks a request against the access control rules to determine what policy would be applied.

Legend:

	#		The rule position in the configuration.
	*		The first fully matched rule.
	~		Potential match i.e. if the user was authenticated they may match this rule.
	hit     The criteria in this column is a match to the request.
	miss    The criteria in this column is not match to the request.
	may     The criteria in this column is potentially a match to the request.

Notes:

	A rule that potentially matches a request will cause a redirection to occur in order to perform one-factor
	authentication. This is so Authelia can adequately determine if the rule actually matches.


```
authelia access-control check-policy [flags]
```

### Options

```
  -c, --config strings    configuration files to load (default [config.yml])
      --groups strings    the groups of the subject
  -h, --help              help for check-policy
      --ip string         the ip of the subject
      --method string     the HTTP method of the object (default "GET")
      --url string        the url of the object
      --username string   the username of the subject
      --verbose           enables verbose output
```

### SEE ALSO

* [authelia access-control](authelia_access-control.md)	 - Helpers for the access control system

###### Auto generated by spf13/cobra on 2-Jun-2022