# npm 2.x shrinkwrap + git deps = expected

This works (modulo the non-idempotent `shrinkwrap` behavior).

```sh
node -v # 4.2.2
npm -v # 2.14.11
npm init
npm cache clean async
npm i -S async
rm -rf node_modules && npm i
npm shrinkwrap && rm -rf node_modules && npm i
npm shrinkwrap # 1: NOT idempotent, no error
npm i -S sindresorhus/get-stream#v1.0.0 && npm shrinkwrap
npm shrinkwrap # 2: idempotent, no error
rm -rf node_modules && npm i
npm shrinkwrap # 3: NOT idempotent, no error
npm shrinkwrap # 4: idempotent, no error
```
