---
layout: default
title: Security
permalink: /guides/security
---

[signing-commits]: https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commit
[ecryptfs]: https://www.ecryptfs.org/
[luks]: https://wiki.archlinux.org/index.php/LUKS
[gpg]: https://www.gnupg.org/
[data-at-rest]: https://en.wikipedia.org/wiki/Data_at_rest
[data-in-transit]: https://en.wikipedia.org/wiki/Data_in_transit

# Security Guidelines

Here are some security recommendations to help the team minimize any possible attack vectors. This list is by no means an exhaustive list of guidelines and will evolve in the future.

## Multi factor authentication(MFA)

We should ensure that MFA is used at all times, limiting any attack surface substantially.

## Passwords

As a team, we do not enforce a password schema, but passwords should be as secure as you deem so; some general guidelines are:

- different from other passwords
- safe from external viewing
- no obvious personal information like your name

## Data

### Sensitive Data

Sensitive data is anything that might risk the company if an external party sees it. This data could be:
- environment variables like secrets, keys, passwords, endpoints, tokens
- customer/partner details
- company assets
- projects

If any company asset is downloaded to a local machine, it should serve its purpose and be deleted from the local machine or encrypted.

### At rest

[Data at rest][data-at-rest] is data when it is not moving. Such as:
- stored on some device
- on some cloud platform
- in a database
- in your browser

There are many risks involved with data at rest:
- physical, such as burglary, robbery, theft
- digital, such as device compromise

In general, the key to mitigating this risk is to ensure that everything is encrypted and unnecessary data is removed when it is no longer needed.

The best-in-class solution for encrypting data at rest is to encrypt the entire drive using something like [LUKS][luks]. This is not always feasible so you can use something like [EcryptFS][ecryptfs] to encrypt individual folders/files. These tools are not exhaustive, there are variants in all operating systems.

Some great tools:
- [GPG][gpg]
- [EcryptFS][ecryptfs]
- [LUKS][luks]

### In transit

[Data in transit][data-in-transit] is any time data is *moving* from one place to another.

Careful consideration should be taken about the data is sent across:
- insecure networks, such as HTTP
- chat apps like slack, discord, telegram
- open networks like coffee shops, restaurants

A note on chat apps:

While not generally insecure, chat apps still open an unnecessary risk of leaked data and open an attack vector of the respective companies' access to our data.

## Logging

Logging is an essential tool in the Development Process. 

It does, however, carry some risk; Developers should take care to ensure that no sensitive data is logged. And any logs are redacted if passed on an insecure channel.

## Git usage

As a team, we need to be mindful of what we commit to the repository, that is, to ensure no secrets or sensitive data gets leaked in a commit. 
If this happens, you must ensure the data is not leaked. Usually, this would be rectifying the leakage and force pushing.

To mitigate this, always make sure you inspect your commits before pushing.

### Commit Verification

All commits should be verified and signed by the person who made the commit.

[Signing commits][signing-commits]

## CI/CD Pipelines

CI/CD pipelines potentially have the most access to a project's data, so we should ensure that we are mindful of what we do with it.

Sometimes troubleshooting might print sensitive data; we should be mindful of:
- if this company is compromised, what would happen if someone were to access our data?

## Social engineering

Teams in the blockchain industry are increasingly subject to social engineering attacks. Be on the lookout for any such behavior like:

- phishing, like dm's, emails, text messages
- over the shoulder theft, like an attacker stealing information from peeking eyes
- imposters, like a fake identity, fake email, fake phone number

## Insider threat

Generally, the tools used are federated, and we have limited risk as long as offboarding processes are taken promptly.

It's still helpful to ensure we manage data responsibly and on a need-to-know basis due to several insider threat attacks simply by the attacker having too much access to too much data.

# Incidents

If an incident happens, we should notify the relevant team of the incident and consider how we might mitigate this in the future in a post-incident review. 

The purpose of the review is not to point fingers but merely to learn what we can do to mitigate the incident.