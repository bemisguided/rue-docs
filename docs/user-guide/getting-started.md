## Installation
Type the following command to install **rue** to your project:
```bash
npm install rue --save
```

## Creating Dependencies
**rue** tries to support a number of injection and activation patterns to ensure
that the configuration is decoupled from application code. One of the most basic
patterns is to leverage the standard nodejs module/packaging system. Take for
example the following modules and **rue** configuration:

```javascript
// MyDependency.js
exports.myFunction = function() {
  console.log('myFunction called');
};
```

The above is a simple nodejs module that will serve as a dependency to the next
nodejs module. It exports a single function called `myFunction()`.

```javascript
// MyModule.js
let myDependency
exports.init = function(_myDependency) {
  this.myDependency = _myDependency;
}
```

The above is another simple nodejs module that will be injected with the
`MyDependency` dependency. It exports a single function called `init()` that
expects a single parameter which will be the injected `MyDependency` instance.

## Configuring Dependencies
Both these nodejs modules are then configured in a separate nodejs module
presented below.

```javascript
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useObject(require('./MyModule'))
  .withDependencies('MyDependency')
  .done();

rue.module('MyDependency')
  .useObject(require('./MyDependency'))
  .done();
```

Here the both the modules are configured into the **rue** dependency injection
container. `MyModule` is defined to resolve to `require('./MyModule')`
and requiring the dependency `MyDependency` while `MyDependency` is defined to
resolve to `require('./MyDependency')`.

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

The above shows how to activate the dependency injection container. Here the
container ensures that dependencies are initialized in the correct order and
injected as defined. Additionally, as dependencies might be initialized
asynchronous, the `activate()` returns a `Promise` to indicate when complete.

The following command would start the application with the following output:

```bash
node rue.js
> myFunction called
> Application has been successfully started
```
