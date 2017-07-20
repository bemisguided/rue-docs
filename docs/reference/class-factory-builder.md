Configures a dependency following the [Factory Injection Pattern](../user-guide/injection-patterns.md#factory-injection).

**Superclasses:**

[Builder](./class-builder.md)

**Subclasses:**

N/A

## .useFunction()
Configures the dependency to be either a singleton or non-singleton managed by
the dependency injection container. By default, all dependencies are singletons
unless configured otherwise.

**Signature:**

```javascript
.useFunction(fn : Function) : Builder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `fn` | `Function` | Required | Factory function to configure this dependency with |

**Return:**

[FactroyBuilder](./class-factory-builder.md) to allow configuration chaining

**Example:**

```javascript hl_lines="5"
// rue.js
const rue = require('rue');

rue.factory('MyFactory')
  .useFunction(require('./MyModule.js').factoryFunction)
  .done();
```
