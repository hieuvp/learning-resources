## Lerna publish

```
lerna publish
```

1. Run <code>lerna updated</code> to check which packages have changed since the last release (last git tag).
2.	If necessary, increment the version key in **lerna.json**.
3.	Update the **package.json** of all updated packages to their new versions.
4.	Update all dependencies of the updated packages with the new versions, specified with a caret (^).
5.	Create a new git commit and tag for the new version.
6.	Publish updated packages to npm.

* Lerna won't publish packages which are marked as <code>"private": true</code> in the **package.json**.
