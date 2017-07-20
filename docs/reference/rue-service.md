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
| `container` | [Container](./class-container.md) | Optional | **rue** dependency injection container to configure the dependency in. If omitted the singleton [rue](./rue.md) container is used |

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
