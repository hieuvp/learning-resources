# Peer Dependencies

## Problem

* **YourCoolProject**
	* JacksModule 1.0
		* JillsModule 1.0
	* JillsModule 2.0

From **YourCoolProject**

```javascript
// This is an instance of JillsClass 2.0
const jillsObject = new JillsClass()
```

From **JacksModule 1.0**

```javascript
// This will be false
// because we are using JillsClass 1.0
jillsObject instanceof JillsClass
```

## Solution

- I need this package, but I need the version that is part of the project, not some version private to my module.
- When npm sees that your package is being installed into a project that does not have that dependency, or that has an incompatible version of it,  it will warn the user during the installation process.

## peerDependencies

* <code>npm install</code> does not install **peerDependencies**.

* **Root project** installs without **peerDependencies**

```
npm WARN react-example@0.1.0 requires a peer of react@^16.0.0 but none is installed. You must install peer dependencies yourself.
npm WARN react-dom@16.2.0 requires a peer of react@^16.0.0 but none is installed. You must install peer dependencies yourself.
```

## Usage

### When

- When you are building a library to be used by other projects, and
- This library is using some other library, and
- You expect/need the user to work with that other library as well.

### Example

**React Component Library**

- Put a <code>react</code> dependency in both **peerDependencies** and **devDependencies**.
- Never put a <code>react</code> dependency in **dependencies**.
- If using **lerna** for managing project, all <code>peer dependencies</code> should be added to root **package.json**.
