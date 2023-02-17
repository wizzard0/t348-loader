# t348-loader
isomorphic (browser, node) TypeScript / JavaScript loader

## Supported Features

- ESM, TypeScript 4.4, JavaScript (ES2021)
- Isomorphic (browser, node), zero dependencies, 321K of readable JS
- Stack traces
- Module packaging/publishing (incomplete)

## Unsupported features

- CommonJS, JSX, TSX
- import cycles (use [madge] to get rid of them, it makes the code cleaner anyway)
- type checking (use the full `tsc` for that)

## Usage 

### Node.js (16, 18)

1. Copy t348.mjs to your project
2. Use `node --experimental-loader=./t348.mjs your-app.ts [args]` to launch your application

### Browsers (ESM only)

1. Add the following to your `HTML`:

```html
<head>
  <script src="t348.mjs" type="module" data-global-repo="./t348repo/t0$HASH.ts"></script>
  <script src="app.js" type="text/typescript"> (OR CODE WITH NEWLINES HERE) </script>
</head>
```

### Browsers: global repository

`TODO document this` (yes it includes incomplete package manager-like functionality)

### Publishing modules

`TODO document this` (TLDR: if you import files by hash, you don't need versions. for public use I need to make hashes longer though, lol)

```sh
export T348_GLOBAL_REPO='https://repo.website/t0$HASH.js'
export T348_GLOBAL_REPO_PUBLISH='https://repo.website/?name=t0$HASH.js'
node t348.mjs t348pack yourModule.js
> t0aAa1bBb2.js
```

```js
import { yourFunction } from 't0aAa1bBb2.js' // will try to resolve from FS first, then from global repo
```

## How it works

Transpiling: manually stripped down [sucrase]@3.21.0

TODO 
- more details
- automate sucrase feature removal, update to latest version
- bring JSX back? (I don't need it. Use [naked-preact] instead)
- more tests

## Detect cycles

```sh
madge --warning --circular --extensions ts,js --image deps-circular.svg <ENTRYPOINT/FOLDER>
```

[madge]: https://github.com/pahen/madge
[sucrase]: https://github.com/alangpierce/sucrase
[naked-preact]: https://github.com/wizzard0/naked-preact
