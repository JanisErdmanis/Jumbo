# JuBox

A Julia distribution for science, out of the box. This is an example repository demonstrating the bundling of a Julia distribution. A Julia distribution is defined by a `Project.toml` file which must contain `name` and `version` fields, similar to Julia packages. All listed packages and dependencies are bundled into the stdlib path, making them resistant to accidental precompilations.

## Building

To run the build, install Julia 1.11 or later and execute the following commands:
```bash
julia --project=meta 
]instantiate
```

Once dependencies are installed, perform the build:
```bash
julia --project=meta meta/build.jl --build-dir=build
```
This creates build artifacts in the `build` directory. By default, the bundle targets the host platform. 

Builds can also be performed with GitLab via Build → Pipelines, where they can be started manually or are initiated when tagging a new release. Note that artifact upload to releases has not yet been tested.

## Cross-platform Builds

You can create bundles for other platforms using command options:
```bash
julia --project=meta meta/build.jl --build-dir=build --target-arch=aarch64 --target-platform=macos --compiled-modules=existing
```

This creates a bundle for the specified platform where precompilation will occur on the user's system at first launch.
