## Reselect

- [**Memoization**](https://en.wikipedia.org/wiki/Memoization) `/ˌmeməaɪˈzeɪʃn/` is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again.

- In **Redux**, whenever an action is called anywhere in the application, all mounted & connected components call their `mapStateToProps` function. This is why [**Reselect**](https://github.com/reduxjs/reselect) is awesome. It will just return the memoized result if nothing has changed.

- A **`Selector`** created with `createSelector` has a cache size of `1` and only returns the cached value when its set of arguments is the same as its previous set of arguments.
