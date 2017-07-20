# FactoryBuilder Class

Configures a dependency following the
[Factory Injection](../user-guide/injection-patterns.md#factory-injection)
pattern. This class is accessible from [rue.factory()](./rue-factory.md).

**Superclasses:**

[Builder](./class-builder.md)

**Subclasses:**

N/A

## Methods

### .useFunction()
Configures the factory function to use for a *Factory* dependency.

**Signature:**

```javascript
.useFunction(fn : Function) : FactoryBuilder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `fn` | `Function` | Required | Factory function to configure the dependency with. |

**Returns:**

[FactoryBuilder](./class-factory-builder.md) to allow configuration chaining

**Example:**

```javascript hl_lines="5"
// rue.js
const rue = require('rue');

rue.factory('MyFactory')
  .useFunction(require('./MyFactory.js').factoryFunction)
  .done();
```
