By default all configured dependencies are required and if **rue** is unable to
resolve a dependency by name on activation it will throw an error indicating
the missing dependency.

Sometimes it is desired that a dependency is optional and this is where **rue**
provides a simple *Dependency Notation* to identify which dependencies are
optional and how to handle them.

- The `?` prefix indicates that the dependency is optional and if it is not
available the dependency parameter is skipped entirely

- The `+` prefix indicates that the dependency is optional and if it is not
available the dependency parameter is replaced with `undefined`

The following example shows a configuration demonstrating both uses of
*Dependency Notation*:

```javascript
// rue.js
const rue = require('rue');

rue.module('ModuleA')
  .useObject(require('./ModuleA'))
  .withDependencies('Dependency1', '?Dependency2', 'Dependency3')
  .done();

rue.module('ModuleB')
  .useObject(require('./ModuleB'))
  .withDependencies('Dependency1', '+Dependency2', 'Dependency3')
  .done();
```

This would result for `ModuleA` to be initialized as follows if `Dependency2`
was unavailable:

```javascript
moduleA.init(dependency1, dependency3);
```

While `ModuleB` would be initialized as follows:

```javascript
moduleB.init(dependency1, undefined, dependency3);
```
