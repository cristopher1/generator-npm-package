<h1 align="center">Welcome to generator-quality-npm-package 👋</h1>
<p>
  <img alt="Version" src="https://img.shields.io/badge/version-0.0.0-blue.svg?cacheSeconds=2592000" />
  <a href="https://github.com/cristopher1/generator-quality-npm-package#readme" target="_blank">
    <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" />
  </a>
  <a href="https://github.com/cristopher1/generator-quality-npm-package/graphs/commit-activity" target="_blank">
    <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  </a>
  <a href="https://github.com/cristopher1/generator-quality-npm-package/blob/master/LICENSE" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/github/license/cristopher1/generator-quality-npm-package" />
  </a>
</p>

> Yeoman generator to create quality npm packages with eslint, prettier, commitlint, husky, babel and other tools.

### 🏠 [Homepage](https://github.com/cristopher1/generator-quality-npm-package)

The `generator-quality-npm-package` provides a structure to create a npm package similar to that used in the: [@cljmenez/json-serializer-vue-localstorage-reactive](https://www.npmjs.com/package/@cljimenez/json-serializer-vue-localstorage-reactive), [@cljimenez/json-serializer-core](https://www.npmjs.com/package/@cljimenez/json-serializer-core) and [@cljimenez/json-serializer-base-serializers](https://www.npmjs.com/package/@cljimenez/json-serializer-base-serializers).
The structure created by this generator includes:

- [Jest](https://jestjs.io/)
- [Babel](https://babeljs.io/) with [@babel/cli](https://babeljs.io/docs/babel-cli), [@babel/core](https://babeljs.io/docs/babel-core),
  [@babel/plugin-transform-runtime](https://babeljs.io/docs/babel-plugin-transform-runtime), [@babel/preset-env](https://babeljs.io/docs/babel-preset-env),
  [@babel/runtime-corejs3](https://www.npmjs.com/package/@babel/runtime-corejs3) and [core-js](https://www.npmjs.com/package/core-js)
- [Eslint](https://eslint.org/) with [eslint-config-prettier](https://www.npmjs.com/package/eslint-config-prettier), [eslint-config-standard](https://www.npmjs.com/package/eslint-config-standard),
  [eslint-plugin-jest](https://www.npmjs.com/package/eslint-plugin-jest), [eslint-plugin-jsdoc](https://www.npmjs.com/package/eslint-plugin-jsdoc), etc.
- [Prettier](https://prettier.io/) with [prettier-plugin-jsdoc](https://www.npmjs.com/package/prettier-plugin-jsdoc)
- [Lint-staged](https://www.npmjs.com/package/lint-staged)
- [Faker](https://fakerjs.dev/)
- [Commitlint](https://commitlint.js.org/#/)
- [Rollup](https://rollupjs.org/) with [@rollup/plugin-babel](https://www.npmjs.com/package/@rollup/plugin-babel), [@rollup/plugin-node-resolve](https://www.npmjs.com/package/@rollup/plugin-node-resolve) and [rollup-plugin-dts](https://www.npmjs.com/package/rollup-plugin-dts)
- [Readme-md-generator](https://github.com/kefranabg/readme-md-generator)
- [Husky](https://www.npmjs.com/package/husky)
- Others

Example of a npm package generated by `generator-quality-npm-package`:

![Captura de pantalla (5)](https://github.com/cristopher1/generator-quality-npm-package/assets/21159930/646f3434-d382-4d3c-a24c-bab8e4841bcd)

This generator uses rollup to create the dist folder. The packages publishes by this generator are exported using the following structure:

package.json

```json
"main": "./dist/cjs/index.cjs",
"types": "./dist/types/index.d.ts",
"exports": {
  "types": "./dist/types/index.d.ts",
  "import": "./dist/esm/index.mjs",
  "require": "./dist/cjs/index.cjs"
},
"files": [
  "dist"
]
```

### [Index](#index)

- [Installation](#installation)
- [The configuration files](#configuration-files)
- [The question: Do you want to automatically run the scripts that configure the package, then installing the dependencies?](#configuring-the-project-automatically)
- [The scripts in package.json](#scripts)
- [Getting To Know Yeoman](#know-yeoman)
- [Author](#author)
- [Contributing](#contributing)
- [Show your support](#support)
- [License](#license)

## <a id="installation"></a> Installation

First, install [Yeoman](http://yeoman.io) and generator-quality-npm-package using [npm](https://www.npmjs.com/) (we assume you have pre-installed [node.js](https://nodejs.org/)).

```bash
npm install -g yo
npm install -g generator-quality-npm-package
```

Then generate your new project:

```bash
yo quality-npm-package
```

## <a id="configuration-files"></a> The configuration files

The configuration files included are:

- Eslint: `.eslintignore` (the files and directories ignored by eslint) and `.eslintrc.json` (configuration used by eslint).
- Git: `.gitignore` (the files and directories ignored by git).
- Lint-staged: `.lintstagedrc.json` (configuration used by lint-staged).
- Prettier: `.prettierignore` (the files and directories ignored by prettier) and `.prettierrc.json` (configuration used by prettier).
- Babel: `babel.config.json` (configuration used by babel):

  - The `env.buildCommonjs` contains the configuration used to transpile the source code to es5. It is used into `rollup.config.js` and `rollup.config.mjs`.

  - The `env.buildESmodules` contains the configuration used to transpile the source code to es6. It is used into `rollup.config.js` and `rollup.config.mjs`.

  - If the package.json, generated by this generator, contains the field `type:commonjs` will be included the `env.test` property in babel.config.json. That property is used by jest to transpile the source code to es5 before to run the tests.

- Commitlint: `commitlint.config.js` (configuration used by commitlint).

- Jest: `jest.config.js` (configuration used by jest).

- Rollup: `rollup.config.js` and `rollup.config.mjs` (configuration used by rollup).

- TypeScript: `tsconfig.json` (configuration used by TypeScript compiler).

## <a id="configuring-the-project-automatically"></a> The question: Do you want to automatically run the scripts that configure the package, then installing the dependencies?

When you selects the true value, the following scripts ubicated in the package.json are executed:

- `init`
- `documentation:create`
- `test`
- `build`

If you selects the false value, you must run `npm run init` obligatory.

## <a id="scripts"></a> The scripts in package.json

The more important scripts added into the package.json created by this generator are:

- `"init"`: Runs the commands necessary to initialize the package, for example `init:husky`.
- `"documentation:create"`: Creates documentation using readme-md-generator.
- `"format"`: Checks the format using prettier.
- `"format:fix"`: Fixes the format using prettier.
- `"format:build-stage"` and `"format:build-stage:fix"`: similar to `"format"` and `"format:fix"`. They used when the `npm run build` is called.
- `"lint"`: static code analysis using eslint.
- `"lint:fix"`: Fixes the code using eslint.
- `"lint:build-stage"` and `"lint:build-stage:fix"`: similar to `"lint"` and `"lint:fix"`. They are used when the `npm run build` is called.
- `"build:bundle"`: Bundles the files into src folder using rollup. It is used when the `npm run build` is called.
- `"build:tsc"`: Generates .d.ts files using the TypeScript compilator. It is used when the `npm run build` is called.
- `"build"`: Generates the dist folder that contains the cjs folder (source code transpiled to es5), the esm folder (source code transpiled to es6), and types folder (it contains the declaration files).
- `"prepublishOnly"`: Used before publishing your package using `npm publish`. Runs `npm run build`.
- `"test"`: Runs the tests using jest.
- `"commitlint"`: Runs commitlint. It is used into .husky/commit-msg file. It is called by the commit-msg hook. See [git hook](https://www.atlassian.com/git/tutorials/git-hooks#:~:text=The%20commit%2Dmsg%20hook%20is,file%20that%20contains%20the%20message.).
- `"lint-staged"`: Runs lint-staged. It is used into .husky/pre-commit file. It is called by the pre-commit hook. See [git hook](https://www.atlassian.com/git/tutorials/git-hooks#:~:text=The%20commit%2Dmsg%20hook%20is,file%20that%20contains%20the%20message.).
- `"quality-check"`: Runs `npm run format && npm run lint && npm run test`. It is used into .husky/pre-push file. It is called by the pre-push hook See [git hook](https://www.atlassian.com/git/tutorials/git-hooks#:~:text=The%20commit%2Dmsg%20hook%20is,file%20that%20contains%20the%20message.).

## <a id="know-yeoman"></a> Getting To Know Yeoman

- Yeoman has a heart of gold.
- Yeoman is a person with feelings and opinions, but is very easy to work with.
- Yeoman can be too opinionated at times but is easily convinced not to be.
- Feel free to [learn more about Yeoman](http://yeoman.io/).

## <a id="author"></a> Author

👤 **Cristopher Jiménez**

- Github: [@cristopher1](https://github.com/cristopher1)

## <a id="contributing"></a> 🤝 Contributing

Contributions, issues and feature requests are welcome!<br />Feel free to check [issues page](https://github.com/cristopher1/generator-quality-npm-package/issues).

## <a id="support"></a> Show your support

Give a ⭐️ if this project helped you!

## <a id="license"></a> 📝 License

Copyright © 2023 [Cristopher Jiménez](https://github.com/cristopher1).<br />
This project is [MIT](https://github.com/cristopher1/generator-quality-npm-package/blob/master/LICENSE) licensed.

---

_This README was generated with ❤️ by [readme-md-generator](https://github.com/kefranabg/readme-md-generator)_
