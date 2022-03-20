---
title: "Security Key"
description: "Authelia utilizes Webauthn security keys as one of it's second first factor authentication methods."
lead: "Authelia utilizes Webauthn security keys as one of it's second first factor authentication methods."
date: 2022-03-19T04:53:05+00:00
lastmod: 2022-03-19T04:53:05+00:00
draft: false
images: []
menu:
  overview:
    parent: "authentication"
weight: 240
toc: true
---
**Authelia** supports hardware-based second factors leveraging [FIDO2]&nbsp;[Webauthn] compatible security keys like
[YubiKey]'s.

Security keys are among the most secure second factor. This method is already supported by many major applications and
platforms like Google, Facebook, GitHub, some banks, and much more.

![YubiKey](yubikey.jpg "A YubiKey Security Key")

Normally, the protocol requires your security key to be enrolled on each site before being able to authenticate with it.
Since Authelia provides Single Sign-On, your users will need to enroll their device only once to get access to all your
applications.

<p align="center">
  <img src="../../images/REGISTER-U2F.png" width="400">
</p>

After having successfully passed the first factor, select *Security Key* method and click on *Register device* link.
This will send you an email to verify your identity.

*NOTE: This e-mail has likely been sent to the mailbox at https://mail.example.com:8080/ if you're testing Authelia.*

Confirm your identity by clicking on **Register** and you'll be asked to touch the token of your security key to
complete the enrollment.

Upon successful enrollment, you can authenticate using your security key by simply touching the token again when
requested:

<p align="center">
  <img src="../../images/2FA-U2F.png" width="400">
</p>

Easy, right?!

## FAQ

### Can I register multiple FIDO2 Webauthn devices?

At present this is not possible in the frontend. However the backend technically supports it. We plan to add this to the
frontend in the near future. Subscribe to [this issue](https://github.com/authelia/authelia/issues/275) for updates.

### Can I perform a passwordless login?

Not at this time. We will tackle this at a later date.

### Why don't I have access to the *Security Key* option?

The [Webauthn] protocol is a new protocol that is only supported by modern browsers. Please ensure your browser is up to
date, supports [Webauthn], and that the feature is not disabled if the option is not available to you in **Authelia**.

### Can my FIDO U2F device operate with Authelia?

At the present time there is no plan to support [FIDO U2F] within Authelia. We do implement a backwards compatible appid
extension within **Authelia** however this only works for devices registered before the upgrade to the [FIDO2]&nbsp;[Webauthn]
protocol.

If there was sufficient interest in supporting registration of old U2F / FIDO devices in **Authelia** we would consider
adding support for this after or at the same time of the multi-device enhancements.

[FIDO U2F]: https://www.yubico.com/authentication-standards/fido-u2f/
[FIDO2]: https://www.yubico.com/authentication-standards/fido2/
[Webauthn]: https://www.yubico.com/authentication-standards/webauthn/
[YubiKey]: https://www.yubico.com/products/yubikey-5-overview/