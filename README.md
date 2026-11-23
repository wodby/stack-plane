# Plane application stack for Kubernetes on Wodby

Deploy Plane project management on Kubernetes with Wodby.

This repository defines the Wodby stack manifests and default service
composition for Plane.

<!-- wodby:generated:start -->

## Stack contract

- [Plane stack on Wodby](https://wodby.com/stacks/plane)
- [Browse Wodby application stacks](https://wodby.com/stacks)
- [Plane stack guide](https://wodby.com/docs/2.0/stacks/catalog/plane/)
- [Wodby stack documentation](https://wodby.com/docs/2.0/stacks/)
- [Stack manifest reference](https://wodby.com/docs/2.0/stacks/template/)

## Service definitions

- [Plane service](https://github.com/wodby/service-plane)
- [PostgreSQL service](https://github.com/wodby/service-postgres)
- [Valkey service](https://github.com/wodby/service-valkey)
- [RabbitMQ service](https://github.com/wodby/service-rabbitmq)
- [Silo service](https://github.com/wodby/service-silo)
- [OpenSMTPD service](https://github.com/wodby/service-opensmtpd)

## What's included

| Component / service | Default configuration |
| --- | --- |
| Plane<br>`plane` | required; enabled by default; links: `db` → `postgres`, `redis` → `valkey`, `amqp` → `rabbitmq`, `storage` → `silo`, `sendmail` → `opensmtpd` |
| PostgreSQL<br>`postgres` | required; enabled by default; volumes: `data` 10 GB |
| Valkey<br>`valkey` | required; enabled by default |
| RabbitMQ<br>`rabbitmq` | required; enabled by default; volumes: `data` 5 GB |
| Silo<br>`silo` | required; enabled by default; volumes: `data` 20 GB |
| OpenSMTPD<br>`opensmtpd` | optional; disabled by default |

Enabled optional services are selected by default but can be excluded when an
app is created. Disabled optional services are available but not selected by
default. Required services cannot be excluded.

## Validate the stack manifest

```bash
wodby stack validate-manifest stack.yml --org <org-id>
```

<!-- wodby:generated:end -->

## Deploy this stack

The stack needs no repository: Plane runs from its own images.

Enter the administrator's email and a strong password in the Plane service's settings when you create the app. The
first deployment installs Plane with that account, so its setup page is never open to visitors; sign in at the app's
address, or at `/god-mode` for instance settings. Sign-up is off unless you turn on the **Allow sign-up** setting.
The first deployment takes several minutes while Plane prepares its database.

Uploaded files and images are stored in Silo, an S3-compatible storage service, and reach browsers through Plane's own
address. Enable OpenSMTPD to send email notifications and invitations.

## Maintain a custom version

1. Fork this repository.
2. Edit the stack manifest.
3. Import the repository as a [Git-backed stack](https://wodby.com/docs/2.0/stacks/create/#create-a-git-backed-stack).

When replacing or renaming a stack service, update every related link target
and derivative reference. Stack-local names and referenced service names are
distinct identifiers.
