# *Prepublish* <br/>[![Sponsored by][sponsor-img]][sponsor] [![Version][npm-version-img]][npm] [![Downloads][npm-downloads-img]][npm] [![Build Status Unix][travis-img]][travis] [![Build Status Windows][appveyor-img]][appveyor] [![Dependencies][deps-img]][deps]

*Prepublish* is a solution for simplifying pre-publishing typical JavaScript projects for publishing to NPM.

[sponsor-img]: https://img.shields.io/badge/Sponsored%20by-Sebastian%20Software-692446.svg
[sponsor]: https://www.sebastian-software.de
[deps]: https://david-dm.org/sebastian-software/prepublish
[deps-img]: https://david-dm.org/sebastian-software/prepublish.svg
[npm]: https://www.npmjs.com/package/prepublish
[npm-downloads-img]: https://img.shields.io/npm/dm/prepublish.svg
[npm-version-img]: https://img.shields.io/npm/v/prepublish.svg
[travis-img]: https://img.shields.io/travis/sebastian-software/prepublish/master.svg?branch=master&label=unix%20build
[appveyor-img]: https://img.shields.io/appveyor/ci/swernerx/prepublish/master.svg?label=windows%20build
[travis]: https://travis-ci.org/sebastian-software/prepublish
[appveyor]: https://ci.appveyor.com/project/swernerx/prepublish/branch/master


## Transpilers

*Prepublish* includes two transpiler configurations:

- **[Buble](https://buble.surge.sh/guide/)**: Blazing fast ES2015+ transpiler where the goal is to have lightweight runtime code, too.
- **[Babel](https://babeljs.io/docs/plugins/preset-latest/)**: Configuration of Babel transpiler. Supports all of ES2015/ES2016/ES2017. Plus some ES3 helpers for maximum engine compatibility. Plus Support for [Object-Rest-Spread](https://babeljs.io/docs/plugins/transform-object-rest-spread/) and [Class Properties](https://babeljs.io/docs/plugins/transform-class-properties/). The High-performance async engine with support for generators and async/await powered by [fast-async](https://github.com/MatAtBread/fast-async) is enabled by default. It requires [nodent-runtime](https://github.com/MatAtBread/nodent-runtime). Uses [Transform-Runtime](https://github.com/babel/babel/tree/master/packages/babel-plugin-transform-runtime) to externalize requirements to Polyfills. Resulting code needs all Polyfills for each library published with this tool. Typically by using services like [polyfill.io](https://qa.polyfill.io/v2/docs/) or [Babel Runtime](https://github.com/babel/babel/tree/master/packages/babel-runtime) aka [CoreJS](https://github.com/zloirock/core-js).


## Output Targets

*Prepublish* produces builds depending on the entries of your packages `package.json`. It supports
building for CommonJS and well as producing output with ES Modules (ESM). Just add the relevant entries to
the configuration.

- CommonJS Output: `main`
- ES Module Output: `module` (`jsnext:main` is deprecated)

To offer separate NodeJS and Browser builds use one of the following keys for the browser bundle: `browser` or `web` or `browserify`. These bundles are always exported as ES Modules (ESM) as we have the assumption that they are bundled by another tool like Webpack or Rollup before usage.

67m8BAQAg4mc
## Classic vs. ES2015 vs. Modern

You are able to export modules for either ES2015 compatible environments or even more modern platforms, too. This happens in parallel and typically requires some heavy lifting on the bundling phase with Webpack, too. This is because we are using non-standardized configuration keys in package.json. Typically just append `:modern` to your normal targets:

- CommonJS Output for NodeJS with ES2015 kept intact: `main:modern`
- ES Modules Output for NodeJS with ES2015 kept intact: `module:modern`
- Browser Output as ES Modules with ES2015 kept intact: `browser:modern`

While `es2015` is exactly a requirement for the client to have full ES2015 support, `modern` is more flexible.
We are thinking of updating what we understand as `modern` regularly. Currently `modern` is not fixed by specific
features.

To make sense of all these new modules it would help to produce two different outputs. One for classic browsers and one for modern browsers. ES2015 enabled features are [rapidly catching up in performance](https://kpdecker.github.io/six-speed/). Some features are pretty hard to rework for older browsers like Generators, Async/Await, or even Block Scope. Therefor we think there is no need for sending modern clients the fully transpiled code down the wire. Keep in mind that you have to implement some basic client detection to send one or the other file to the matching client.

BTW: The modern builds [make a lot of sense during development](https://medium.com/@gajus/dont-use-babel-transpilers-when-debugging-an-application-890ee528a5b3) as it results in shorter transpiler runtimes.


## Articles

- [Setting up multi-platform npm packages](http://2ality.com/2017/04/setting-up-multi-platform-packages.html)



## Installation

### NPM

```console
$ npm install --save-dev prepublish
```

### Yarn

```console
$ yarn add --dev prepublish
```



## Usage

*Prepublish* comes with a binary which can be called from within your `scripts` section
in the `package.json` file.

```json
"scripts": {
  "prepare": "prepublish"
}
```

There is also some amount of parameters you can use if the auto detection of your library does not work out correctly.

```
Options
  --entry-node      Entry file for NodeJS target [default = auto]
  --entry-web       Entry file for Browser target [default = auto]
  --entry-binary    Entry file for Binary target [default = auto]

  --output-folder   Configure the output folder [default = auto]

  -t, --transpiler  Chose the transpiler/config to use. Either "babel" or "buble". [default = babel]
  -x, --minified    Enabled minification of output files
  -m, --sourcemap   Create a source map file during processing

  -v, --verbose     Verbose output mode [default = false]
  -q, --quiet       Quiet output mode [default = false]
```


## Contributing

* Pull requests and stars are always welcome.
* For bugs and feature requests, please create an issue.
* Pull requests must be accompanied by passing automated tests (`$ npm test`).


## License

[Apache License; Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0)


## Copyright

<img src="assets/sebastiansoftware.png" alt="Sebastian Software GmbH Logo" width="250" height="200"/>

Copyright 2016-2017<br/>[Sebastian Software GmbH](http://www.sebastian-software.de)
