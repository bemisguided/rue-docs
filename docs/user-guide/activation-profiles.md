**rue** supports the concept of *Activation Profiles* to enable injection of
different dependencies based on the configuration of the runtime environment.
For example, one *Activation Profile* could be defined for production while
another for testing where stubs or mocks are used on the later.

The following is an example configuration that utilizes *Activation Profiles*:

```javascript hl_lines="6 11"
// rue.js
const rue = require('rue');

rue.module('DatabaseConnection')
  .useModule('./production/DatabaseConnection')
  .withProfiles('production')
  .done();

rue.module('DatabaseConnection')
  .useModule('./test/StubDatabaseConnection')
  .withProfiles('test')
  .done();

rue.service('MyService')
  .useObject('./services/MyService')
  .withDependencies('DatabaseConnection')
  .done();
```

Here the dependency `DatabaseConnection` is configured to use the production
module when the `production` profile is active while a stub is used when the
`test` profile is active. When no profiles are defined the dependency is
available under all profiles, therefore, `MyService` is always available.

The following example shows how the `production` profile is activated using the
**rue** dependency injection container:

```javascript hl_lines="4"
// rue.js
const rue = require('rue');

rue.activate('production')
  .then(() => {
    console.log('Application has been successfully started');
  })
  .catch((error) => {
    console.log('Application has failed to be started', error);    
  });
```

*Activation Profiles* allows for a dependency to be enabled with the absence
of a profile by using the not operator (`!`) as part of the declaration.

The following example shows how a dependency is configured when the `test`
profile is *not* active:

```javascript hl_lines="5"
const rue = require('rue');

rue.module('DatabaseConnection')
  .useModule('./production/DatabaseConnection')
  .withProfiles('!test')
  .done();
```

*Activation Profiles* can be activated at runtime by environment variables. By
utilizing the environment variable `RUE_PROFILES` with a comma separated list
of profiles **rue** will resolve these profiles for activation. For example,
`export RUE_PROFILES=production,staging` would enable the profiles `production`
and `staging`.

Additionally, **rue** recognizes the environment variable `NODE_ENV` – made
popular by numerous nodejs libraries such as [express](http://expressjs.com/)
– which is resolved to a profile names prefixed be `env:`. For example
`export NODE_ENV=production` resolves to `env:production`.

The following example shows how runtime environment variable profiles are
configured:

```javascript hl_lines="4"
// rue.js
const rue = require('rue');

rue.activate(rue.environment.profiles())
  .then(() => {
    console.log('Application has been successfully started');
  })
  .catch((error) => {
    console.log('Application has failed to be started', error);    
  });
```
!!! seealso "See Also"
    [Environment.profiles()](../reference/class-environment.md) in the
    *Reference* section.
