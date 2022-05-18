---
title: "Cloudflare Zero Trust"
description: "Integrating Cloudflare Zero Trust with Authelia via OpenID Connect."
lead: ""
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

{{< community-doc >}}

## Tested Versions

- Authelia: v4.35.5

## Before You Begin

You are required to utilize a unique client id and a unique and random client secret for all [OpenID Connect] relying
parties. You should not use the client secret in this example, you should randomly generate one yourself. You may also
choose to utilize a different client id, it's completely up to you.

This example makes the following assumptions:

- **Cloudflare Team Name:** `example-team`
- **Authelia Root URL:** `https://auth.example.com`
- **Client ID:** `cloudflare`
- **Client Secret:** `cloudflare_client_secret`

## Configuration

### Application

To configure [Cloudflare Zero Trust] to utilize Authelia as an [OpenID Connect] Provider:

1. Visit the [Cloudflare Zero Trust Dashboard](https://dash.teams.cloudflare.com)
2. Visit `Settings`
3. Visit `Authentication`
4. Under `Login nethods` select `Add new`
5. Select `OpenID Connect`
6. Enter the following values:
   1. Name: `Authelia`
   2. App ID: `cloudflare`
   3. Client Secret: `cloudflare_client_secret`
   4. Auth URL: `https://auth.example.com/api/oidc/authorization`
   5. Token URL: `https://auth.example.com/api/oidc/token`
   6. Certificate URL: `https://auth.example.com/jwks.json`
   7. Add the following OIDC Claims: `preferred_username`, `mail`, `groups`
7. Click Save

### Authelia

The following YAML configuration is an example **Authelia**
[client configuration](../../../configuration/identity-providers/open-id-connect.md#clients) for use with [Cloudflare]
which will operate with the above example:

```yaml
- id: cloudflare
  secret: cloudflare_client_secret
  public: false
  authorization_policy: two_factor
  scopes:
    - openid
    - profile
    - groups
    - email
  redirect_uris:
    - https://example-team.cloudflareaccess.com/cdn-cgi/access/callback
  userinfo_signing_algorithm: none
```

## See Also

- [Cloudflare Zero Trust Generic OIDC Documentation](https://developers.cloudflare.com/cloudflare-one/identity/idp-integration/generic-oidc/)

[Cloudflare]: https://www.cloudflare.com/
[Cloudflare Zero Trust]: https://www.cloudflare.com/products/zero-trust/
[OpenID Connect]: ../../openid-connect/introduction.md