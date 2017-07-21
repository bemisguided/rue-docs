# Environment Class

Provides hooks to the runtime environment for **rue**.

## Static Methods

### .profiles()
Returns an array of the *Activation Profiles* that were resolved at runtime.

This method extracts profiles from the environment variable `RUE_PROFILES`
which can be a comma separated list of profile names. For example,
`RUE_PROFILES=profile1,profile2` would add the profiles `profile1` and
`profile2` to the resulting array.

Additionally, this method extracts the environment variable `NODE_ENV` – made
popular by numerous nodejs libraries such as [express](http://expressjs.com/) – 
to resolve a runtime profile. The value of this environment variable will be
prefixed with `env:`. For example, `NODE_ENV=production` would add the profile
`env:profile` to the resulting array.

**Signature:**

```javascript
.profiles() : Array<string>
```

**Parameters:**

N/A

**Returns:**

`Array<string>` an array instance of the profile names resolved

**Example:**

```javascript hl_lines="4"
// rue.js
const rue = require('rue');

let profiles = rue.environment.profiles();

rue.activate(profiles)
  .then(() => {
    console.log('Application has been successfully started');
  })
  .catch((error) => {
    console.log('Application has failed to be started', error);    
  });
```
