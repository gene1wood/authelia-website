---
title: "Portainer"
description: "Integrating Portainer with Authelia via OpenID Connect."
lead: "This documentation is maintained by the community. If you find an error with this documentation please either make a pull request or start a GitHub Discussion."
date: 2022-03-19T04:53:05+00:00
lastmod: 2022-03-19T04:53:05+00:00
draft: false
images: []
menu:
  integration:
    parent: "openid-connect"
weight: 420
toc: true
---


## Tested Versions

- Authelia: v4.34.6
- Portainer (CE and EE): 2.12.2

## Before You Begin

You are required to utilize a unique client id and a unique and random client secret for all OpenID Connect relying
parties. You should not use the client secret in this example, you should randomly generate one yourself. You may also
choose to utilize a different client id, it's completely up to you.

In this example makes the following assumptions:

- **Application Root URL:** `https://portainer.example.com`
- **Authelia Root URL:** `https://auth.example.com`
- **Client ID:** `portainer`
- **Client Secret:** `portainer_client_secret`

## Configuration

### Application

To configure [Portainer] to utilize Authelia as an OpenID Connect Provider:

1. Visit Settings
2. Visit Authentication
3. Select:
   1. Authentication Method: OAuth
   2. Provider: Custom
   3. Enable *Automatic User Provision* if you want users to automatically be created in [Portainer].
4. Configure the following:
   1. Client ID: `portainer`
   2. Client Secret: `portainer_client_secret`
   3. Authorization URL: `https://auth.example.com/api/oidc/authorization`
   4. Access Token URL: `https://auth.example.com/api/oidc/token`
   5. Resource URL: `https://auth.example.com/api/oidc/userinfo`
   6. Redirect URL: `https://portainer.example.com`
   7. User Identifier: `preferred_username`
   8. Scopes: `openid profile groups email`


{{< figure src="portainer.png" alt="Portainer" width="736" style="padding-right: 10px" >}}

### Authelia

The following YAML configuration is an example **Authelia**
[client configuration](../../../configuration/identity-providers/open-id-connect.md#clients) for use with [Portainer]
which will operate with the above example:

```yaml
- id: portainer
  secret: portainer_client_secret
  public: false
  authorization_policy: two_factor
  scopes:
    - openid
    - profile
    - groups
    - email
  redirect_uris:
    - https://portainer.example.com
  userinfo_signing_algorithm: none
```

[Portainer]: https://www.portainer.io/