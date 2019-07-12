# Repro for issue importing json module across project boundary in Yarn monorepo (incremental compilation)

This repo is a minimal case that exhibits the following traits:

- It is a Yarn monorepo with two packages:

  - `packages/main`, this one imports a JSON file from:
  - `packages/strings`

Each package is its own TypeScript project, and takes advantage of TypeScript incremental compilation.

In order to see

- Run `yarn` to install `typescript`
- `yarn repro` to reproduce the issue. This runs the following commands:

  1. `yarn clean` - removes all build artifacts
  2. `yarn build` - the first build succeeds
  3. `yarn build` - the second one fails!

Note that the `packages/main/tsconfig.json` project has `packages/strings/tsconfig.json` listed as a reference; however, `tsc` still complains that the main project doesn't have `foo.json` in its project file list.

```
> yarn repro
yarn run v1.16.0
$ yarn run clean && yarn run build && yarn run build
$ find . -iname 'lib' -type d | grep -v node_modules | xargs rm -rf
$ tsc --build .
$ tsc --build .
error TS6307: File '<project-dir>/packages/strings/lib/foo.json' is not in project file list. Projects must list all files or use an 'include' pattern.


Found 1 error.
```
