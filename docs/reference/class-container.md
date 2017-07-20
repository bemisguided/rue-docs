# Container Class
Main **rue** dependency injection container.

## Static Properties

### .singleton
The singleton instance of the **rue** dependency injection container.

**Signature:**

```javascript
.singleton : Container
```

**Returns:**

[Container](./class-container.md) singleton container instance

**Example:**

```javascript hl_lines="4"
// rue.js
const rue = require('rue');

let container = rue.Container.singleton;
let promise = container.getInstance('name');
```
## Methods

### .activate()
Activates the dependency injection container for a given array of activation
profiles names.

**Signature:**

```javascript
.activate(... profileNames : string) : Promise<Map<string, ?>>
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `profileNames` | `... string` | Optional | One or more activation profile names. |

**Returns:**

`Promise<Map<string, ?>>` promise that resolves to a map of all singleton
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

### .getInstance()

!!! warning "Unstable"
    **As of 0.9.0:** this method is likely to change in the next version.

### .getDependencies()

!!! warning "Unstable"
    **As of 0.9.0:** this method is likely to change in the next version.

### .replaceInstance()
Replaces an active dependency instance with another instance. This replacement
will be available immediately to any dependency into which it was injected.

Replacement instances can only be assigned to singleton dependencies or the
dependencies of singletons. For example, dependency `DependencyA` is a singleton
it is dependent upon `DependencyB` which is a non-singleton. Either
`DependencyA` can be replaced directly or `DependencyB` can be replaced with
`DependencyA` as the parent dependency.

!!! note "Note"
    Only dependencies that resolve to either an Object or Function can be
    replaced. Dependencies that are scalar types (i.e. string, number, etc)
    cannot be replaced after activation. This is because scalar types cannot
    be proxied using ES6 Proxies.

**Signature:**

```javascript
.replaceInstance(name: string, replacement: ?, [parent: string]) : void
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `name` | `string` | Required | Name of the dependency to replace. |
| `replacement` | `?` | Required | Instance to use as a replacement. |
| `parent` | `string` | Optional | Owning dependency name of the dependency to be replaced. |

**Returns:**

N/A

**Example:**

```javascript hl_lines="6"
// rue.js
const rue = require('rue');

let replacement = {};

rue.replaceInstance('MyDependency', replacement);
```
