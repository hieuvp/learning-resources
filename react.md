## Reselect

- In **Redux**, whenever an action is called anywhere in the application, all mounted & connected components call their `mapStateToProps` function. This is why [`reselect `](https://github.com/reduxjs/reselect) is awesome. It will just return the memoized result if nothing has changed.
- A selector created with `createSelector` has a cache size of `1` and only returns the cached value when its set of arguments is the same as its previous set of arguments.
