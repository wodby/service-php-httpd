# Apache HTTP server (PHP) service for Kubernetes on Wodby

Run Apache HTTP server (PHP) as a reusable Kubernetes application service with
Wodby.

This repository defines the Wodby service manifests and operational
configuration for Apache HTTP server (PHP).

- [Browse Wodby services](https://wodby.com/services)
- [Wodby service documentation](https://wodby.com/docs/2.0/services/)
- [Service manifest reference](https://wodby.com/docs/2.0/services/template/)

## Wodby stacks using this service

- [PHP application stack](https://github.com/wodby/stack-php)

## Service overview

| Property | Manifest configuration |
| --- | --- |
| Service name | `php-httpd` |
| Type | Application service |
| Inherits from | [`httpd`](https://github.com/wodby/service-httpd) with version constraint `^1.0.0` |
| Workloads | `main` (Deployment), primary |
| Containers | `apache` |
| Service links | Backend, optional |
| Application build | Dockerfile: `Dockerfile` |
| Configuration | 1 settings |

## Use this service

Use this service through [PHP application stack](https://github.com/wodby/stack-php), or reference `php-httpd` from a
custom Wodby stack.

A service is a reusable component and does not deploy by itself. The stack
defines its links, settings, versions, resources, and relationship to the rest
of the application.

## Maintain a custom version

1. Fork this repository.
2. Edit the service manifest and referenced files.
3. Import the repository as a [Git-backed service](https://wodby.com/docs/2.0/services/create/#create-a-git-backed-service).
4. Reference the service from a stack manifest.

Keep service, workload, container, endpoint, link, volume, config, and
derivative names stable unless dependent stacks and app-level overrides are
updated at the same time.

Validate the manifests with:

```bash
wodby service validate-manifest service.yml --org <org-id>
```

See the [service manifest reference](https://wodby.com/docs/2.0/services/template/) and the [managed services index](https://github.com/wodby/services).
