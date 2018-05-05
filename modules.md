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

1. Simple calculator:

	```javascript
	// calculator.js
	
	const add = (a, b) => a + b;
	
	module.exports.add = add;
	```

2. Node.js internally wraps all require()-ed modules in a function wrapper:

	```javascript
	(function (exports, require, module, __filename, __dirname) {
	
	  // calculator.js is actually executed here
	  module.exports.add = (a, b) => a + b;
	
	});
	```

3. Variable "**module**" is an object representing the current module. It is local to each module and it is also **private** (only accessible from module code):

```javascript
console.log(module);

Module {
  id: '/Volumes/Data/Workspace/Experiment/kafka/calculator.js',
  exports: { add: [Function] },
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

- `exports` is a reference to the `module.exports`, a convenience variable to help module authors write less code. Working with its properties is safe and recommended.

For example:

```javascript
exports.add = add;

module.exports.add = add;
```

Be aware:

```javascript
// Exported from require of module
module.exports.add = add;

// Not exported, only available in the module
exports = { add };
```

- It is common practice to replace module.exports with custom functions or objects. If we do that but still would like to keep using the "exports" shorthand; then "exports" must be re-pointed to our new custom object:

// TODO: write example why need to re-assign

```javascript
exports = module.exports = {}

exports.method = function() {...}
```

## require()

There is nothing special about require. It’s an object that acts mainly as a function that takes a module name or path and returns the module.exports object. We can simply override the require object with our own logic if we want to.

For testing
// When you call require(), you don't get an instance of the module.
// You get an object with references to the module's functions.
// If you overwrite a value in the required module, your own reference is overwritten,
// but the implementation keeps the original references

## Manual mocks (Jest)

## Resources

- [Node.js Documentation](https://nodejs.org/api/modules.html)
- [Node.js module.exports vs. exports](https://medium.freecodecamp.org/node-js-module-exports-vs-exports-ec7e254d63ac)
- [The Node.js Way - How `require()` Actually Works](http://fredkschott.com/post/2014/06/require-and-the-module-system/)
- [Requiring modules in Node.js: Everything you need to know](https://medium.freecodecamp.org/requiring-modules-in-node-js-everything-you-need-to-know-e7fbd119be8)
