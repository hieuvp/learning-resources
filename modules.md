# Modules

## Table of Contents

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [The module wrapper](#the-module-wrapper)
- [The module Object](#the-module-object)
- [exports](#exports)
- [require()](#require)
- [Manual mocks (Jest)](#manual-mocks-jest)
- [Resources](#resources)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## The module wrapper

```javascript
// calculator.js

const add = (a, b) => a + b;

module.exports.add = add;
```

Before a module's code is executed, Node.js will wrap it with a function wrapper that looks like the following:

```javascript
(function (exports, require, module, __filename, __dirname) {
  // Module code actually lives in here

  const add = (a, b) => a + b;

  module.exports.add = add;
});
```

## The module Object

```javascript
// calculator.js

const add = (a, b) => a + b;

module.exports.add = add;

console.log(module);
```

When this module is called by `index.js`:

```javascript
Module {
  id: '/Volumes/Data/Workspace/Experiment/kafka/calculator.js',
  exports: { add: [Function: add] },
  parent: 
   Module {
     id: '.',
     exports: {},
     parent: null,
     filename: '/Volumes/Data/Workspace/Experiment/kafka/index.js',
     loaded: false,
     children: [ [Circular] ],
     paths: 
      [ '/Volumes/Data/Workspace/Experiment/kafka/node_modules',
        '/Volumes/Data/Workspace/Experiment/node_modules',
        '/Volumes/Data/Workspace/node_modules',
        '/Volumes/Data/node_modules',
        '/Volumes/node_modules',
        '/node_modules' ] },
  filename: '/Volumes/Data/Workspace/Experiment/kafka/calculator.js',
  loaded: false,
  children: [],
  paths: 
   [ '/Volumes/Data/Workspace/Experiment/kafka/node_modules',
     '/Volumes/Data/Workspace/Experiment/node_modules',
     '/Volumes/Data/Workspace/node_modules',
     '/Volumes/Data/node_modules',
     '/Volumes/node_modules',
     '/node_modules' ] }
```

## exports

- `exports` is a **reference** to the `module.exports`, a convenience variable to help module authors write less code.

```javascript
exports.add = add;

// Identical to

module.exports.add = add;
```

- Be aware

```javascript
// Never exported, reference to module.exports is lost

exports = { add };
```

## require()

- An object that acts mainly as a function that **takes** a `module name` or `path` and **returns** the `module.exports` object.

- Be aware

```javascript
// calculator.js

const log = (a, b, sum) => {
  console.log(`Calculator Logger: ${a} + ${b} = ${sum}`);
};

const add = (a, b) => {
  const sum = a + b;
  log(a, b, sum);
  return sum;
};

module.exports = { log, add };
```

```javascript
// index.js

const calculator = require('./calculator');

// Calculator Logger: 2 + 3 = 5
calculator.add(2, 3);

// Reason
calculator.log = () => {
  console.log('New Logger');
};

// New Logger
calculator.log();

// Calculator Logger: 2 + 3 = 5
calculator.add(2, 3);
```

When Node invokes that `require()` function with a local file path as the function’s only argument, Node goes through the following sequence of steps:

1. **Resolving**: To find the absolute path of the file.
1. **Loading**: To determine the type of the file content.
1. **Wrapping**: To give the file its private scope. This is what makes both the `require` and `module` objects local to every file we require.
1. **Evaluating**: This is what the VM eventually does with the loaded code.
1. **Caching**: So that when we require this file again, we don’t go over all the steps another time.

## Manual mocks (Jest)

For testing
// When you call require(), you don't get an instance of the module.
// You get an object with references to the module's functions.
// If you overwrite a value in the required module, your own reference is overwritten,
// but the implementation keeps the original references


## Resources

- [Node.js Documentation](https://nodejs.org/api/modules.html)
- [Node.js module.exports vs. exports](https://medium.freecodecamp.org/node-js-module-exports-vs-exports-ec7e254d63ac)
- [The Node.js Way - How `require()` Actually Works](http://fredkschott.com/post/2014/06/require-and-the-module-system/)
- [Requiring modules in Node.js: Everything you need to know](https://medium.freecodecamp.org/requiring-modules-in-node-js-everything-you-need-to-know-e7fbd119be8)
