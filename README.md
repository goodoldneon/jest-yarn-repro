## Yarn Workspace Issue Repro

This is a repro for Yarn workspaces improperly handling transitive dependencies.

## Initial Setup

`yarn install`

## Repro

Running `yarn workspace workspace-b jest --version` shows version `24.9.0` even though `27.0.1` is specified in `workspace-b/package.json`. Version `24.9.0` is actually a transitive dependency from `babel-plugin-optimize-hook-destructuring`.

This might be a `nodeLinker` bug. When `nodeLinker: "node-modules"`:

```
$ yarn workspace workspace-b jest --version
24.9.0
```

When `nodeLinker: "pnp"`:

```
$ yarn workspace workspace-b jest --version
27.0.3
```
