---
title: "Kubernetes"
description: "An introduction into integrating Authelia with Kubernetes."
lead: "An introduction into integrating Authelia with Kubernetes."
date: 2022-03-19T04:53:05+00:00
lastmod: 2022-03-19T04:53:05+00:00
draft: false
images: []
menu:
  integration:
    parent: "kubernetes"
weight: 310
toc: true
---

{{< figure src="kubernetes.png" alt="Kubernetes" width="100" style="padding-right: 10px" >}}

## UNDER CONSTRUCTION

The following areas are actively being worked on for Kubernetes:

1. Detailed Documentation
2. [Helm Chart](https://github.com/authelia/chartrepo) for Helm v3 see our [chart repository](https://charts.authelia.com)
3. Kustomize Deployment
4. Manifest Examples

Users are welcome to reach out directly by using any of our various [contact options](../../information/contact.md).

## Important Notes

The following section has special notes regarding utilizing Authelia with Kubernetes.

1. Authelia (and all of your other applications) may receive an invalid remote IP if the service handling traffic to
   the Kubernetes Ingress of your choice doesn't have the `externalTrafficPolicy` setting configured to `local` as per
   the Kubernetes [preserving the client source ip] documentation.
2. Authelia's configuration management system conflicts with the `enableServiceLinks` option when it's set to `true`
   which is the default. This should be changed to `false`. See the
   [PodSpec v1 core](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#podspec-v1-core) documentation
   for more details.

## FAQ

### RAM usage

If using file-based authentication, the argon2id provider will by default use 1GB of RAM for password generation. This
means you should allow for at least this amount in your deployment/daemonset spec and have this much available on your
node, alternatively you can
[tweak the providers settings](https://www.authelia.com/docs/configuration/authentication/file.html#memory). Otherwise,
your Authelia may OOM during login. See [here](https://github.com/authelia/authelia/issues/1234#issuecomment-663910799)
for more info.

[preserving the client source ip]: https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/#preserving-the-client-source-ip