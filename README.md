# Example how to make Semantic Release with Lerna nad Conventional Commits

Boilerplate used in article [Semantic Release with Lerna and Conventional Commits](https://michaljanaszek.com/blog/lerna-conventional-commits)

Code used in this repo is based on [reggi/lerna-tutorial](https://github.com/reggi/lerna-tutorial)

## Lerna commands and weird behaviour

Make a change to `@my-scope/beta` (e.g. "fix: my minor change").

Run `lerna diff`:

```diff
lerna notice cli v3.13.1
lerna info versioning independent
diff --git a/packages/beta/index.js b/packages/beta/index.js
index a0a991d..e03c90d 100644
--- a/packages/beta/index.js
+++ b/packages/beta/index.js
@@ -1 +1 @@
-module.exports = 'world?!?';
+module.exports = 'World?!?';
```

This indicates only `beta` has a changes.

`beta` now has a version of `1.1.3` and is defined as a dependency of `usage` with `"@my-scope/beta": "<3.0.0"` there should be no change to `usage`.

However, `lerna publish` generates a new version for `usage`:

```
lerna notice cli v3.13.1
lerna info versioning independent
lerna info Looking for changed packages since @my-scope/usage@1.1.3
lerna info getChangelogConfig Successfully resolved preset "conventional-changelog-angular"

Changes:
 - @my-scope/beta: 1.1.3 => 1.1.4
 - @my-scope/usage: 1.1.3 => 1.1.4

? Are you sure you want to publish these packages?
```

If we select `Yes` the dependency is changed to `"@my-scope/beta": "^1.1.4"` incorrectly.
