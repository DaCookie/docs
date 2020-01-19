# Documentations - Node JS - Link a local package

As an example, assume to have a local npm package named "dummy".

Go to the project that contain this package:

```bash
npm link
```

Then, go to the project, and link the original projet using its name:

```bash
npm link dummy
```

Note that the project won't appear in your `node_modules` folder, unless it requires a dependency.

It also won't appear in your `package.json`.

---

See official documentation from: [https://docs.npmjs.com/cli/link.html](https://docs.npmjs.com/cli/link.html)

[<= Back to summary](./README.md)