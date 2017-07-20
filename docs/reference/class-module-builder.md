Configures a dependency following the
[Module Injection](../user-guide/injection-patterns.md#module-injection)
pattern. This class is accessible from [rue.module()](./rue-module.md).

**Superclasses:**

[Builder](./class-builder.md)

**Subclasses:**

N/A

## Public Methods

### .lifecycleInit()
Configures the name of the initialization function for the *Module* dependency.
By default, the initialization function is `init()` unless configured otherwise.

**Signature:**

```javascript
.lifecycleInit(name : string) : ModuleBuilder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `name` | `string` | Required | Name of the initialization function. |

**Returns:**

[ModuleBuilder](./class-module-builder.md) to allow configuration chaining

**Example:**

```javascript hl_lines="6"
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useObject(require('./MyModule.js').factoryFunction)
  .lifecycleInit('start')
  .done();
```

### .useObject()
Configures the module to use for a *Module* dependency.

**Signature:**

```javascript
.useObject(object : Object) : ModuleBuilder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `object` | `Object` | Required | Module object to configure the dependency with. |

**Returns:**

[ModuleBuilder](./class-module-builder.md) to allow configuration chaining

**Example:**

```javascript hl_lines="5"
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useObject(require('./MyModule.js').factoryFunction)
  .done();
```
