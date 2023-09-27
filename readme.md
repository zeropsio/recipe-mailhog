# MailHog Zerops Recipe

[MailHog](https://github.com/mailhog/MailHog) is simple, yet powerful email testing tool for developers written in Go.

This repository contains utility recipe for deploying MailHog into [Zerops](https://zerops.io).

## Quick Install

### GUI method

Paste the following yaml into the [Zerops GUI](https://app.zerops.io/dashboard/projects) (_Your Project > Import services_):

```yaml
services:
  - hostname: mailhog
    type: go@1
    envVariables:
      MH_CORS_ORIGIN: "*"
      MH_HOSTNAME: mailhog.zerops
      MH_STORAGE: maildir
      MH_MAILDIR_PATH: /var/www/maildir
    ports:
      - port: 8025
      - port: 1025
        httpSupport: false
    minContainers: 1
    maxContainers: 1
    buildFromGit: https://github.com/zeropsio/recipe-mailhog@v2
    enableSubdomainAccess: true
```

### ZCLI method

Clone this repository and use [`zcli`](https://github.com/zeropsio/zcli) to import MailHog service to an already existing project:

```bash
zcli service import <project-name> import-services.yml 
```

### For absolute newcomers

Paste the contents of [import-project.yaml](https://github.com/zeropsio/recipe-mailhog/blob/v2/import-project.yml) into the [Zerops GUI](https://app.zerops.io/dashboard/projects) (_Import a project_) and see the magic happens :)

## Usage and Configuration

You can access the SMTP server mock on `mailhog:1025` (by default). You can change the SMTP listening address by introducing `MH_SMTP_BIND_ADDR` environment variable.

[comment]: <> (TODO: Refer to the docs > environment variables section.)

Test the installation by running:

```shell
/usr/sbin/sendmail -S mailhog:1025
```

...or maybe by adding the following line to php.ini:

```
sendmail_path = /usr/sbin/sendmail -S mailhog:1025
```

## Further Customization

For further configuration of MailHog using environment variables, please refer to the [official MailHog .md file](https://github.com/mailhog/MailHog/blob/master/docs/CONFIG.md).

**Forks and pull requests with improvements and bug fixes are welcomed! :)**

## Known Issues

- Stored emails are lost after service deletion or re-build. Solution might be adding MongoDB as email storage. Coming soon...
