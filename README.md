# PublicJuliaRegistry
For use with LocalRegistry.jl

The following tutorial is based on Fedora Linux. Let `user` denote the linux user.

### To create a new registry
In the Julia REPL, do:
```
using LocalRegistry
create_registry("PublicJuliaRegistry", "https://github.com/RoyCCWang/PublicJuliaRegistry",
description = "Public unregistered Julia packages")
```

### From a fresh install of Julia, add an existing GitHub registry, like this one.
For HTTPS GitHub access.
```
using Pkg
pkg"registry add https://github.com/RoyCCWang/PublicJuliaRegistry"
# this is only for HTTP.
```
For SSH access:
```
pkg"registry add git@github.com:RoyCCWang/PublicJuliaRegistry.git"
```

### Check which registries are currently in use
`Pkg.Registry.status()` to check which registries are used. By default, Julia ships with the `General` registry.

### To add unregistered packages to a registry
To add to the registry, need to add the package (e.g. the `Utilities` packages mentioned below) via Pkg's `dev` instead of `Pkg.add` first. Remove the `dev` package once this procedure is done if you don't need Utilities in dev mode.
Example for adding three unregistered packages to the `PublicJuliaRegistry` registry.

```
using LocalRegistry
register("Utilities";
registry = "PublicJuliaRegistry",
repo = "https://gitlab.com/RoyCCWang/utilities")

register("ProbabilityUtilities";
registry = "PublicJuliaRegistry",
push = true,
repo = "https://gitlab.com/RoyCCWang/probabilityutilities")

register("RiemannianOptim";
registry = "PublicJuliaRegistry",
push = true,
repo = "https://gitlab.com/RoyCCWang/riemannianoptim")
```

### To update the version and compatibility meta info of a package that is already in a registry
Once you make changes to a package that is listed in a registry, you might update its release number or other meta info. To incorporate this information into the registry:
Make sure the latest version of the package of interest (e.g. Utilities in the example below) is installed in Julia locally via Pkg's `dev` instead of `add`.
The following would update the meta data of the `Utilities` package to whichever URL/location that is installed locally in dev mode.

```
using LocalRegistry
register("Utilities")
```
