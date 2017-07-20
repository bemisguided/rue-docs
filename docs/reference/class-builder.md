Base class for all **rue** configuration builders.

**Superclasses:**

N/A

**Subclasses:**

[FactoryBuilder](./class-factory-builder.md),
[ModuleBuilder](./class-moduel-builder.md),
[ServiceBuilder](./class-service-builder.md)

## Public Methods

### .done()

### .isSingleton()
Configures the dependency to be either a singleton or non-singleton managed by
the dependency injection container. By default, all dependencies are singletons
unless configured otherwise.

**Signature:**

```javascript
.isSingleton(singleton : boolean) : Builder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `singleton` | `boolean` | Required | `true` indicates the dependency is a singleton. |

**Returns:**

[Builder](./class-builder.md) to allow configuration chaining

**Example:**

```javascript hl_lines="6"
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useObject(require('./MyModule.js'))
  .isSingleton(false)
  .done();
```

### .lifecyclePostInit()

name

### .lifecyclePreDeinit()

name

### .lifecycleDeinit()

name

### .withDependencies()

... dependencyNames

### .withProfiles()

... profileNames
