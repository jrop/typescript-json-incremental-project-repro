# Repro for issue importing json module across project boundary

- Run `yarn` or `npm i` to install `typescript`
- `yarn repro`/`npm run repro` to reproduce the issue

Note that the `src/main/tsconfig.json` project has `src/strings/tsconfig.json` listed as a reference; however, `tsc` still complains that the main project doesn't have `foo.json` in its project file list.

```
> yarn repro
yarn run v1.13.0
$ tsc -b ./src
error TS6307: File 'd:/vso/typescript-json-project/src/strings/foo.json' is not in project file list. Projects must list all files or use an 'include' pattern.


Found 1 error.
```