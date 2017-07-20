| Lifecycle | Default Name | Configurator | Details |
| --------- | ------------ | ------------ | ------- |
| **Initialization** | `init` | `lifecycleInit()` | Used to accept the injection of dependencies and initialize the dependency. **Only applicable to Module injection pattern.** |
| **Post-Initialization** | `postInit` | `lifecyclePostInit()` | Called after a dependency has been initialized. |
| **Pre-Deinitialization**  | `preDeinit` | `lifecyclePreDeinit()` | Called before a dependency is deinitialized. |
| **Deinitialization**  | `deinit` | `lifecycleDeinit()` | Called to deinitialize a dependency. |

!!! bug "Coming Soon"
    **Not available in 0.9.0:** The lifecycle handling of
    *Pre-Deinitialization* and *Deinitialization* are features that are
    currently under development.
