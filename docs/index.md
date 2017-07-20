**rue** a not (too) opinionated dependency injection container for nodejs

[![npm](https://img.shields.io/npm/v/rue.svg)](https://www.npmjs.com/package/rue)
[![state](https://img.shields.io/badge/state-alpha-yellow.svg)](https://github.com/bemisguided/rue)
[![npm](https://img.shields.io/npm/l/rue.svg)](https://github.com/bemisguided/rue)
[![node](https://img.shields.io/node/v/rue.svg)](https://github.com/bemisguided/rue)
[![David](https://img.shields.io/david/bemisguided/rue.svg)](https://github.com/bemisguided/rue)
[![Build Status](https://travis-ci.org/bemisguided/rue.svg)](https://travis-ci.org/bemisguided/rue)

# Overview

**rue** is a dependency injection container for nodejs that borrows concepts from
both [AngularJS](https://angularjs.com) and [Spring Framework](https://springframework.org).
At the core of **rue** is the goal to decouple configuration and application code.
One should be able to easily add **rue** to an existing project or conversly
remove it without having to greatly re-tool the main application code.

## Features
The core features of **rue** are as follows:

- Dependency injection with minimalistic configuration
- Configuration is decoupled and unintrusive from application code
- Module, service and factory patterns supported
- Singleton and non-singleton patterns supported
- Asynchronous activation and/or deactivation of dependencies with Promises support
- Separate activation profiles
- Leverages ES6 Proxies to enable swapping mocks and stubs for testing

## Additional Features
**rue** can offer more features by using the various extension libraries:

- **rue-config** - configuration management and injection
- **rue-route** - route configuration and injection
- **rue-logging** - logging injection 
