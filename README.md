# Rollup peerDependencies issue

### Intro

Rollup seems to get confused when peer dependencies and local packages are involved.

In this example, we have three things:

- app
- package foo
- package bar

App has both packages `foo` and `bar` installed as dependencies. `bar` has zero dependencies, but `foo` has `bar` as a peer dependency.

App will not succesfully compile with Rollup, even though both packages are installed in `node_modules`.

### Output

```
❯ npm run build

> monorepo-test-app@1.0.0 build /Users/arggh/sandbox/rollup-peerdeps-issue/app
> rollup -c


src/main.js → dist/bundle.js...
(!) Unresolved dependencies
https://rollupjs.org/guide/en/#warning-treating-module-as-external-dependency
@monorepo-test/bar (imported by ../packages/foo/index.js)
(!) Missing global variable name
Use output.globals to specify browser global variable names corresponding to external modules
@monorepo-test/bar (guessing 'bar$1')
created dist/bundle.js in 32ms
```

### How to run

```
git clone git@github.com:arggh/rollup-peerdeps-issue.git peerdeps-issue
cd peerdeps-issue/app
npm install
npm run build
```

