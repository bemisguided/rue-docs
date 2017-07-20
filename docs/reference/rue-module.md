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
| `container` | [Container](./class-container.md) | Optional | **rue** dependency injection container to configure the dependency in. If omitted the singleton [rue](./rue.md) container is used |

**Returns:**

[ModuleBuilder](./class-module-builder.md) to complete the configuration via chaining

**Example:**

```javascript hl_lines="4"
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useObject(require('./MyModule.js'))
  .done();
```
