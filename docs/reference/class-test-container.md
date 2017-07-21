#TestContainer Class

Manages the testing states for a **rue** dependency injection container.

**Superclasses:**

N/A

**Subclasses:**

N/A

## Constructor

### new TestContainer()

**Signature:**
```javascript
new TestContainer(container: ?Container);
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `container` | [Container](./class-container.md) | Optional | Container to manage test state for. If omitted the singleton **rue** dependency injection container is used. |


## Methods

### .swap()
Swaps a dependency to allow for stubbing or mocking in tests. When tests are
complete the corresponding [resetSwaps()](#resetswaps) can be called to
revert to the original dependency state of the dependency injection container.

!!! seealso "See Also"
    This functionality relies on [Container.replaceInstance()](./class-container.md#replaceinstance).

**Signature:**

```javascript
.swap(name: string, replacement: any, parent: ?string) : void
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `name` | `string` | Required | Name of the dependency to swap. |
| `replacement` | `any` | Required | Instance to use as a replacement. |
| `parent` | `string` | Optional | Owning dependency name of the dependency to be swapped. |

**Returns:**

N/A

**Example:**

```javascript hl_lines="8"
// rue.js
const rue = require('rue');

let container = new rue.Container();
let testContainer = new TestContainer(container);
let stub = {};

testContainer.swap('MyDependency', stub);
```
