# rue Module

## Properties

### .environment
Access the static
[Environment](./class-environment.md) instance for runtime environment
functionality.

**Signature:**

```javascript
rue.environment : Environment
```

**Returns:**

[Environment](./class-environment.md) static instance

**Example:**

```javascript hl_lines="4"
// rue.js
const rue = require('rue');

let profiles = rue.environment.profiles();
rue.activate(profiles)
  .then(() => {
    console.log('Application has been successfully started');
  })
  .catch((error) => {
    console.log('Application has failed to be started', error);    
  });
```

### .test
Access the [TestContainer](./class-test-container.md) for the singleton **rue**
dependency injection container.

**Signature:**

```javascript
rue.test : Environment
```

**Returns:**

[TestContainer](./class-test-container.md) singleton instance

**Example:**

```javascript hl_lines="4"
// rue.js
const rue = require('rue');

let testContainer = rue.test;
let stub = {};
testContainer.swap('name', stub);
```

## Methods

### .activate()
Activates the singleton dependency injection container for a given array of
activation profiles names.

**Signature:**

```javascript
.activate(... profileNames : string) : Promise<Map<string, any>>
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `profileNames` | `... string` | Optional | One or more activation profile names. |

**Returns:**

`Promise<Map<string, any>>` promise that resolves to a map of all singleton
activated dependencies.

**Example:**

```javascript hl_lines="4"
// rue.js
const rue = require('rue');

rue.activate('profile1', 'profile2')
  .then(() => {
    console.log('Application has been successfully started');
  })
  .catch((error) => {
    console.log('Application has failed to be started', error);    
  });
```

### .factory()
Starts the configuration of a dependency following the
[Factory Injection](../user-guide/injection-patterns.md#factory-injection)
pattern.

**Signature:**

```javascript
rue.factory(name : string, container: Container) : FactoryBuilder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `name` | `string` | Required | Name of the dependency. |
| `container` | [Container](./class-container.md) | Optional | **rue** dependency injection container to configure the dependency in. If omitted the singleton **rue** dependency injection container is used. |

**Returns:**

[FactoryBuilder](./class-factory-builder.md) to complete the configuration via chaining

**Example:**

```javascript hl_lines="4"
// rue.js
const rue = require('rue');

rue.factory('MyFactory')
  .useFunction(require('./MyFactory.js').factoryFunction)
  .done();
```

### .module()
Starts the configuration of a dependency following the
[Module Injection](../user-guide/injection-patterns.md#module-injection)
pattern.

**Signature:**

```javascript
rue.module(name : string, container: Container) : FactoryBuilder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `name` | `string` | Required | Name of the dependency. |
| `container` | [Container](./class-container.md) | Optional | **rue** dependency injection container to configure the dependency in. If omitted the singleton **rue** dependency injection container is used. |

**Returns:**

[ModuleBuilder](./class-module-builder.md) to complete the configuration via chaining

**Example:**

```javascript hl_lines="4"
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useModule(require('./MyModule.js'))
  .done();
```

### .service()
Starts the configuration of a dependency following the
[Service Injection](../user-guide/injection-patterns.md#service-injection)
pattern.

**Signature:**

```javascript
rue.service(name : string, container: Container) : FactoryBuilder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `name` | `string` | Required | Name of the dependency. |
| `container` | [Container](./class-container.md) | Optional | **rue** dependency injection container to configure the dependency in. If omitted the singleton **rue** dependency injection container is used. |

**Returns:**

[ServiceBuilder](./class-service-builder.md) to complete the configuration via chaining

**Example:**

```javascript hl_lines="4"
// rue.js
const rue = require('rue');

rue.service('MyService')
  .useObject(require('./MyService.js'))
  .done();
```

## Classes

### Container
Access to the [Container](./class-container.md) class.

**Signature:**

```javascript
rue.Container : Container
```
**Parameters:**

N/A
