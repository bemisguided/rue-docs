# Builder Class

Base class for all **rue** configuration builders.

**Superclasses:**

N/A

**Subclasses:**

[FactoryBuilder](./class-factory-builder.md),
[ModuleBuilder](./class-moduel-builder.md),
[ServiceBuilder](./class-service-builder.md)

## Methods

### .done()
Completes the configuration for the dependency being declared.

**Signature:**

```javascript
.done() : void
```

**Parameters:**

N/A

**Returns:**

N/A

**Example:**

```javascript hl_lines="6"
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useModule(require('./MyModule.js'))
  .done();
```

### .isSingleton()
Configures whether the dependency being declared is either a singleton or
non-singleton. By default all dependencies are singletons unless configured
otherwise.

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
  .useModule(require('./MyModule.js'))
  .isSingleton(false)
  .done();
```

### .lifecyclePostInit()
Configures the name of the *Lifecycle Post-Initialization* function for the
dependency being declared. By default the post-initialization function is
`postInit()` unless configured otherwise.

**Signature:**

```javascript
.lifecyclePostInit(name : string) : Builder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `name` | `string` | Required | Name of the post-initialization function. |

**Returns:**

[Builder](./class-builder.md) to allow configuration chaining

**Example:**

```javascript hl_lines="6"
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useModule(require('./MyModule.js'))
  .lifecyclePostInit('afterStart')
  .done();
```

### .lifecyclePreDeinit()
Configures the name of the *Lifecycle Pre-Deinitialization* function for the
dependency being declared. By default the pre-deinitialization function is
`preDeinit()` unless configured otherwise.

!!! bug "Coming Soon"
    **Not available in 0.9.0:** The lifecycle handling of
    *Pre-Deinitialization* is currently under development.

**Signature:**

```javascript
.lifecyclePreDeinit(name : string) : Builder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `name` | `string` | Required | Name of the pre-deinitialization function. |

**Returns:**

[Builder](./class-builder.md) to allow configuration chaining

**Example:**

```javascript hl_lines="6"
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useModule(require('./MyModule.js'))
  .lifecyclePreDeinit('beforeStop')
  .done();
```

### .lifecycleDeinit()
Configures the name of the *Lifecycle Deinitialization* function for the
dependency being declared. By default the deinitialization function is
`deinit()` unless configured otherwise.

!!! bug "Coming Soon"
    **Not available in 0.9.0:** The lifecycle handling of *Deinitialization*
    is currently under development.

**Signature:**

```javascript
.lifecycleDeinit(name : string) : Builder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `name` | `string` | Required | Name of the deinitialization function. |

**Returns:**

[Builder](./class-builder.md) to allow configuration chaining

**Example:**

```javascript hl_lines="6"
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useModule(require('./MyModule.js'))
  .lifecycleDeinit('stop')
  .done();
```

### .withDependencies()
Configures the dependency names and the order to provide them to the dependency
being declared.

Dependency names can be provided using
[Dependency Notation](../user-guide/dependency-notation.md) to indicate optional
dependencies.

**Signature:**

```javascript
.withDependencies(... dependencyNames : string) : Builder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `dependencyNames` | `...string` | Required | One or more dependency names. |

**Returns:**

[Builder](./class-builder.md) to allow configuration chaining

**Example:**

```javascript hl_lines="6"
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useModule(require('./MyModule.js'))
  .withDependencies('dependency1', '+dependency2', '+dependency3')
  .done();
```

### .withProfiles()
Configures the profiles with which the dependency being declared should be
activated.

Profiles that are prefixed with the not operator (`!`) indicate that the
declared dependency should be activated when that profile is not activated.

!!! seealso "See Also"
    [Activation Profiles](../user-guide/activation-profiles.md) in the *User
    Guide* section.

**Signature:**

```javascript
.withProfiles(... profileNames : string) : Builder
```

**Parameters:**

| Name | Type | Attribute | Description |
| ---- | ---- | --------- | ----------- |
| `profileNames` | `...string` | Required | One or more profile names. |

**Returns:**

[Builder](./class-builder.md) to allow configuration chaining

**Example:**

```javascript hl_lines="6"
// rue.js
const rue = require('rue');

rue.module('MyModule')
  .useModule(require('./MyModule.js'))
  .withProfiles('profile1', '!profile2')
  .done();
```
