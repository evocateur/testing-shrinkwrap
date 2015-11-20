# npm 3.5.0 shrinkwrap + git deps = :(

This branch merely verifies that `npm@3.5.0` does not fix this issue.

```sh
node -v # 5.1.0
npm -v # 3.5.0
npm init
npm cache clean async
npm i -S async
rm -rf node_modules && npm i
npm shrinkwrap && rm -rf node_modules && npm i
npm shrinkwrap # 1: idempotent, no error
npm i -S sindresorhus/get-stream#v1.0.0 && npm shrinkwrap
rm -rf node_modules && npm i
npm shrinkwrap # 2: error
```

The relevant [`npm-debug.log`](./npm-debug.log) is included.
There seems to be something fishy going on during dependency resolution.
