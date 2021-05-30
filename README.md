## Yarn Workspace Issue Repro

This is a repro for Yarn workspaces improperly handling transitive dependencies.

## Initial Setup

`yarn install`

## Repro

Running `yarn workspace workspace-b jest --version` shows version `24.9.0` even though `27.0.1` is specified in `workspace-b/package.json`. Version `24.9.0` is actually a transitive dependency from `babel-plugin-optimize-hook-destructuring`.

This is happening because `node_modules/.bin/jest` is version `24.9.0`. The desired version is actually in `./node_modules/jest/node_modules/.bin/jest`.

Using my system `yarn` (by commenting out `yarnPath` in `.yarnrc.yml`) fixes the problem by creating `workspace-b/node_modules/.bin/jest` and `workspace-c/node_modules/.bin/jest`. Not sure why my system `yarn` (version `2.4.0`) doesn't have this problem.
