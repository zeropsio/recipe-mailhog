# MailHog Zerops Recipe

Simple recipe for deploying [MailHog](https://github.com/mailhog/MailHog) instance into [Zerops](https://zerops.io).

> MailHog is an email testing tool for developers.

## Quick Install

You can either paste the following yaml into Zerops GUI 

```yaml
project:
  name: mailhog-example
  tags:
    - mailhog
services:
  - hostname: mailhog
    type: go@1
    envVariables:
      # Please refer to https://github.com/mailhog/MailHog/blob/master/docs/CONFIG.md
      # for more advanced configuration settings.
      MH_CORS_ORIGIN: "*"
      MH_HOSTNAME: mailhog.zerops
    ports:
      - port: 8025
        httpSupport: true
      - port: 1025
        httpSupport: true
    minContainers: 1
    maxContainers: 1
    buildFromGit: https://github.com/zeropsio/recipe-mailhog@v2
    enableSubdomainAccess: true
```

or clone this repository and use [`zcli`](https://github.com/zeropsio/zcli), running:

```bash
zcli project import import-project.yml 
```

### Adding MailHog to an existing Zerops project

To add MailHog to an existing Zerops project, run:

```bash
zcli service import <project-name> import-service.yml 
```
