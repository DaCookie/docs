# Documentations - Node JS - Deploy a package using TypeScript

## Installations

```bash
npm init
npm install --save-dev typescript
npm install --save-dev @types/node
npm install --save-dev tslint @muffin-dev/tslint-config

#one-line
npm install --save-dev typescript && npm install --save-dev @types/node && npm install --save-dev tslint @muffin-dev/tslint-config
```

---

## Create and setup tsconfig.json file:

```bash
node node_modules/typescript/bin/tsc --init
```

```json
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
        "declaration": true,
        "outDir": "./",
        "strict": true
    },
    "include": ["src"],
    "exclude": ["node_modules"]
}
```

* `target`: Target compatibility output
* `module`: Set the compatibility libraries
* `declaration`: When generating package, this setting must be set to `true`. It requires from TypeScript to generate definition files (`*.d.ts`) so the package can be used in TypeScript projects as well as native JavaScript
* `outDir`: Defines the path where built files are exported
* `include`: Defines the folders and files to be compiled
* `exclude`: Defines the folders and files to exclude from compilation

---

## Create a `tslint.json` file at the project root, and write linting settings:

```json
{
    "rules": {
        "no-console": false
    },
    "extends": [
        "tslint:recommended",
        "@muffin-dev/tslint-config"
    ]
}
```

* `rules`: Contains all the custom and overriding rules
* `extends`: Defines the rules to use, from existing modules

---

## Setup basic project:

```
/src
    /bin
    /doc
    /lib
    index.ts
package.json
README.md
tsconfig.json
tslint.json
```

### `/src/index.ts`

```ts
export * from './lib/index';

```

### `src/lib/index.ts`

```ts
export class Test { }

```

---

## Update `package.json` file:

```json
"bin": "bin/cli.js",
"directories": {
    "bin": "./bin",
    "doc": "./doc",
    "lib": "./lib"
},
"files": [
    "bin/**/*",
    "doc/**/*",
    "lib/**/*",
    "index.d.ts",
    "index.js"
],
"main": "lib/index.js"
"scripts": {
    "build": "tsc",
    "lint": "tslint -p tsconfig.json",
    "prepublishOnly": "npm run lint",
    "prepare": "npm run build",
    "preversion": "npm run lint"
},
"types": "lib/index.d.ts"
```

Keys:

* `bin`: You can rermove it if your package won't contain custom console commands
* `directories`: You can remove `bin` and `doc` values if your package won't contain custom console commands or public documentation
* `files`: You can remove `bin/**/*` and `doc/**/*` values if your package won't contain custom console commands or public documentation

Commands:

* `prepublishOnly`: This command is called before `prepare`, when you use `npm publish`
* `prepare`: This command is called before the package is packed and published, and when a user installs that package
* `preversion`: This command is called before sending a new version of this package

---

## Final touch

Create a `.gitignore` file:

```
node_modules
/lib
/bin
/doc
```

---

## Log into *npm*, then publish the package:

```bash
npm login
npm publsh
```

[<= Back to summary](./README.md)