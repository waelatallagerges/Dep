---
id: dev-guide-ljm
title: Modifying lib-DEP 
---

# Modifying `lib-DEP `

By default the library is referenced as a prebuilt artifact in a GitHub release. Packages are NOT published to npm. The default dependency path in package.json is:

```json
"lib-DEP ": "https://github.com/DEP/lib-DEP /releases/download/v<version>+<commit-hash>/lib-DEP .tgz)",
```

To work with local copy you may change the path to:

```json
"lib-DEP ": "file:///Users/name/local-lib-DEP -packed-copy.tgz",
```

In order to create the packed file run `npm pack` in the lib-DEP  project directory.

To make the project you must force it to take the sources as 'npm update':

```
npm install lib-DEP  --force && make
```

Or if you are making only changes to the library:

```
npm install lib-DEP  --force && make deploy-lib-DEP 
```

Alternative way is to use [npm link](https://docs.npmjs.com/cli/link).
It allows to link `lib-DEP ` dependency to local source in few steps:

```bash
cd lib-DEP 

#### create global symlink for lib-DEP  package
npm link

cd ../DEP 

#### create symlink from the local node_modules folder to the global lib-DEP  symlink
npm link lib-DEP 
```

:::note
Linking will not work when building the mobile applications.
:::

After changes in your local `lib-DEP ` repository, you can rebuild it with `npm run build` and your `DEP ` repository will use that modified library:

```bash
cd node_modules/lib-DEP 
npm run build
```

If you do not want to use local repository anymore you should run:

```bash
cd DEP 
npm unlink lib-DEP 
npm install
```
