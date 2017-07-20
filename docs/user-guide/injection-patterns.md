**rue** supports three core injection patterns: *Module* (as presented above),
*Service*, and *Factory*. This offers greater flexibility in terms of how to
enable dependency injection into an application.

## Module Injection
The *Module* inject pattern essentially leverages the standard nodejs
module/packaging system. In order to receive injected dependency a module need
only to export a single function that accepts the dependencies as parameters. By
default the expected name for this function is `init()`, however, the name can
be changed when configured with **rue**.

The following example shows how the `init()` function can be renamed to
`start()`:

```javascript hl_lines="6"
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useObject(require('./MyModule'))
  .lifecycleInit('start')
  .done();
```

!!! seealso "See Also"
    [rue.module()](../reference/rue-module.md) and 
    [ModuleBuilder](../reference/class-module-builder.md) in the *Reference*
    section for all configuration options available to the *Module Injection*
    pattern.

The `init()` function can be synchronous or asynchronous. When asynchronous the
`init()` function need only to return a `Promise` and **rue** will wait for the
`Promise` to complete before moving to the next dependency to initialize. This
ensures that all injected dependencies are fully activated for use prior to
being injected to another dependency.

The following example shows how a `Promise` might be used with the `init()`
function to connect to a database:

```javascript
// MyModule.js
const db = require('somedblib');

exports.init = function(myDependency) {
  return new Promise((resolve, reject) => {
    db.connect('some database settings', (error, result) => {
      if (error) {
        return reject(error);
      }
      resolve();      
    })
  });
}

```

As nodejs modules are essentially singleton instances all nodejs modules
configured in this matter are managed singletons by **rue**.

## Service Injection
The *Service Injection* pattern essentially constructs an instance of the
dependency by passing injected dependencies via the constructor.

The following example shows how a *Service* might be defined using the ES6
`class` syntax and the corresponding **rue** configuration:

```javascript
// MyService.js
class MyService {

  constructor(myDependency) {
    this.myDependency = myDependency;
  }

}

module.exports = MyService;

// rue.js
const rue = require('rue');

rue.service('MyService')
  .useObject(require('./MyService.js'))
  .withDependencies('MyDependency')
  .done();
```

!!! seealso "See Also"
    [rue.service()](../reference/rue-service.md) and
    [ServiceBuilder](../reference/class-service-builder.md) in the *Reference*
    section for all configuration options available to the *Service Injection*
    pattern.

By default all *Service* dependencies are managed by **rue** as singletons,
however, this can be overridden so that prior to being injected to other
dependencies a new instance is constructed.

The following example shows how a *Service* is configured to be a non-singleton:

```javascript hl_lines="7"
// rue.js
const rue = require('rue');

rue.service('MyService')
  .useObject(require('./MyService.js'))
  .withDependencies('MyDependency')
  .isSingleton(false)
  .done();
```

## Factory Injection
The *Factory* inject pattern takes a factory function that receives the injected
dependencies and returns the dependency to injection to other dependencies.

The following example shows how a *Factory* might be defined and the
corresponding **rue** configuration:

```javascript
// MyFactory.js
module.exports = function(myDependency) {
  return {
    myFunction: () => {
      return myDependency.myFunction();
    }
  }
}

// rue.js
const rue = require('rue');

rue.factory('MyFactory')
  .useFunction(require('./MyFactory.js'))
  .withDependencies('MyDependency')
  .done();
```

!!! seealso "See Also"
    [FactoryBuilder](../reference/class-factory-builder.md) in the *Reference*
    section for all configuration options available to the *Factory Injection*
    pattern.

The factory function can be synchronous or asynchronous. When asynchronous the
factory function need only to return a `Promise` and **rue** will wait for the
`Promise` to complete before moving to the next dependency to initialize. This
ensures that all injected dependencies are fully activated for use prior to
being injected to another dependency.

The following example shows how a `Promise` might be used with the factory
function to connect to a database:

```javascript
// MyModule.js
const db = require('somedblib');

exports.buildDatabaseConnection = function(myDependency) {
  return new Promise((resolve, reject) => {
    db.connect('some database settings', (error, result) => {
      if (error) {
        return reject(error);
      }
      resolve(db);
    })
  });
}

```

By default all *Factory* dependencies are managed by **rue** as singletons,
however, this can be overridden so that prior to being injected to other
dependencies a the factory function is called to retrieve a new instance.

The following example shows how a *Factory* is configured to be a non-singleton:

```javascript hl_lines="7"
// rue.js
const rue = require('rue');

rue.factory('MyService')
  .useFunction(require('./MyFactory.js'))
  .withDependencies('MyDependency')
  .isSingleton(false)
  .done();
```
