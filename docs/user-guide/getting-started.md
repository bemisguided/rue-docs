## Installation
Type the following command to install **rue** to your project:
```bash
npm install rue --save
```

## Creating Dependencies
**rue** tries to support a number of injection and instantiation patterns to
ensure that the configuration is decoupled from application code. One of the
most basic patterns is to leverage the standard nodejs module/packaging system.

Let's start with the following two simple nodejs modules:

```javascript
// mydependency.js
exports.myFunction = function() {
  console.log('myFunction called');
};
```

This is a simple nodejs module that will serve as a dependency to the next
nodejs module. It exports a single function called `myFunction()`.

```javascript
// mymodule.js
let myDependency

exports.init = function(_myDependency) {
  myDependency = _myDependency;
}
```

This is another simple nodejs module that will be injected with the
`myDependency` dependency. It exports a single function called `init()` that
expects a single parameter which will be the injected `myDependency` instance.

## Configuring Dependencies
Both the above nodejs modules are to be configured in a separate nodejs module
presented below.

```javascript
// rue.js
const rue = require('rue');

rue.module('myModule')
  .useModule(require('./mymodule'))
  .withDependencies('myDependency')
  .done();

rue.module('myDependency')
  .useModule(require('./mydependency'))
  .done();
```

Here the both the modules are configured into the **rue** dependency injection
container. `myModule` is defined to resolve to `require('./mymodule')`
and requiring the dependency `myDependency` while `myDependency` is defined to
resolve to `require('./mydependency')`.

## Container Activation
Finally, the dependency injection container needs to be activated:

```javascript
// rue.js
const rue = require('rue');

rue.activate()
  .then(() => {
    console.log('Application has been successfully started');
  })
  .catch((error) => {
    console.log('Application has failed to be started', error);    
  });
```

This example shows how to activate the dependency injection container. Here the
container ensures that dependencies are initialized in the correct order and
injected as defined. Additionally, as dependencies might be initialized
asynchronous, the `activate()` returns a `Promise` to indicate when complete.

The following command would start the application with the following output:

```bash
node rue.js
> myFunction called
> Application has been successfully started
```
