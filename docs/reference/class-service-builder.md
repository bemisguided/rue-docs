# ServiceBuilder Class

Configures a dependency following the
[Service Injection](../user-guide/injection-patterns.md#service-injection)
pattern. This class is accessible from [rue.service()](./module-rue.md#service).

## Methods

### .useObject()
Configures the class or Object to use for a *Service* dependency.

**Signature:**

```javascript
.useObject(object : Object) : ServiceBuilder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `object` | `Object` | Required | Class or Object to configure the dependency with. |

**Returns:**

[ServiceBuilder](./class-service-builder.md) to allow configuration chaining

**Example:**

```javascript hl_lines="5"
// rue.js
const rue = require('rue');

rue.service('MyService')
  .useObject(require('./MyService.js'))
  .done();
```
