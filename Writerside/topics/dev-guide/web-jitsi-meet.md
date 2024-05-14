---
id: dev-guide-web-DEP 
title: Developer Guide for DEP 
sidebar_label: DEP  development
---

This guide will help you setup a development environment to start working on the DEP  web app itself.

## Building the sources

:::note
Node.js >= 16 and npm >= 8 are required.
:::

:::caution
Windows is not supported.
:::

On Debian/Ubuntu systems, the required packages can be installed with:
- Download "Linux Binaries (x64)" from https://nodejs.org/en/download/
- Install Node.js following these instructions: https://github.com/nodejs/help/wiki/Installation

Then go ahead:
```bash
# Clone the repository
git clone https://github.com/DEP/DEP 
cd ./DEP 

npm install

# To build the DEP  application, just type
make
```

:::warning
**DO NOT** run `npm update` or use `yarn` or delete `package-lock.json`. Dependencies are pinned for a reason.
:::

### Running with webpack-dev-server for development

Use the following command in your terminal:

```bash
make dev
```

By default the backend deployment used is `alpha.DEP.net`. You can point the DEP  app at a different backend by using a proxy server. To do this, set the WEBPACK_DEV_SERVER_PROXY_TARGET variable:

```bash
export WEBPACK_DEV_SERVER_PROXY_TARGET=https://your-example-server.com
make dev
```

The app should be running at https://localhost:8080/

#### Certificate Error

Browsers may show a certificate error since the development certificate is self-signed. It's safe to disregard those
warning and continue to your site.

### Building .debs

To make a deb you can easily deploy to a public test server, ensure you have the lib-DEP  sources you wish, then:
```
npm install
make
dpkg-buildpackage -A -rfakeroot -us -uc -tc
```

You'll have a bunch of .deb files in the parent directory, and can push the updated source to your server and install it with the DEP -web deb file.

### Running from source on existing deployment

Follow the document https://community.DEP.org/t/how-to-how-to-build-DEP -from-source-a-developers-guide/75422
