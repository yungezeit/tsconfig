# @yungezeit/tsconfig

Personal `tsconfig.json` files to extend from.

## Install

```bash
# using pnpm
pnpm add -D @yungezeit/tsconfig
# using npm
npm add -D @yungezeit/tsconfig
# using yarn
yarn add -D @yungezeit/tsconfig
# using bun
bun add -D @yungezeit/tsconfig
```

## Configs

You may extend from the following provided tsconfigs:

**Node:**

```json
{
  "extends": ["@yungezeit/tsconfig/default.json"],
}
```

**Browser:**

```json
{
  "extends": ["@yungezeit/tsconfig/dom.json"],
}
```

## Usage

You should make sure to specify the `include` field in your `tsconfig.json`:

```json
{
  "extends": ["@yungezeit/tsconfig/default.json"],
  "include": ["src/**/*"]
}
```

Usually, one would have secondary `tsconfig` files dedicated to node tooling that are used to match TypeScript files which are not part of the project's actual code. Most of the time, such file are called `tsconfig.{xxx}.json` and should be referenced from the main `tsconfig.json` file:

**`tsconfig.json`**
```json
{
  "extends": "@yungezeit/tsconfig/default.json",
  "references": [{ "path": "./tsconfig.node.json" }],
  "include": ["src/**/*"]
}
```

**`tsconfig.node.json`**
```json
{
  "extends": "./tsconfig.json",
  "include": ["tsup.config.ts", "vitest.config.ts"],
  "compilerOptions": {
    "composite": true,
    "noEmit": false,
    "emitDeclarationOnly": true
  }
}
```