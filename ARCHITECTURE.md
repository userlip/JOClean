# Architecture

## Overview

`jo-clean-berlin.de` is a static website made up of HTML, CSS, JavaScript, and image files. Ploi manages the site and deploys the repository's `main` branch to `/home/ploi/jo-clean-berlin.de`.

Nginx uses that deployment directory as its document root and serves the files directly. There is no application server in the request path.

```text
Browser
  |
  +-- page and asset requests --> nginx --> /home/ploi/jo-clean-berlin.de
  |
  +-- contact form submission --> https://send.marin.sh/api/client/email/joclean
```

## Runtime and data services

The site does not use Laravel or another PHP application runtime. It also has no application database, queue worker, scheduler, or application cache. Any PHP-FPM reload retained in the Ploi deployment script is not required to serve this site.

## External contact-form service

The contact forms submit directly from the browser to the externally hosted endpoint:

```text
https://send.marin.sh/api/client/email/joclean
```

This service is not hosted in this repository or on the site's nginx request path. An outage or incompatible change at that endpoint affects contact-form delivery but does not prevent nginx from serving the static website.

## Operations

- Site manager: Ploi
- Deployment source: GitHub `main` branch
- Nginx document root: `/home/ploi/jo-clean-berlin.de`
- Nginx error log: `/var/log/nginx/jo-clean-berlin.de-error.log`

Deployment-script details are documented in [`docs/deployment.md`](docs/deployment.md).
