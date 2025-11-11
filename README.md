# JuBox

A Julia distribution for science, out of the box. This is an example repository demonstrating the bundling of a Julia distribution. A Julia distribution is defined by a `Project.toml` file which must contain `name` and `version` fields, similar to Julia packages. All listed packages and dependencies are bundled into the stdlib path, making them resistant to accidental precompilations.

## Installation

*The following instructions are for end users installing your built applications.*

- **MSIX (Windows)**: If self-signed, go to MSIX bundle properties and add the certificate to the trusted certificate authorities first (see https://www.advancedinstaller.com/install-test-certificate-from-msix.html). Then double-click on the installer and install the app.
- **Snap (Linux)**: The snap can be installed from a command line: `snap install --classic --dangerous MyApp.snap`
- **DMG (macOS)**: If self-signed, you need to click on the app first, then go to `Settings -> Privacy & Security`, whitelisting the launch request. Then drag and drop the application to the `Applications` folder. Launch the application and go again to `Settings -> Privacy & Security` to whitelist it.

Note that all these extra steps are avoidable with investment in Windows and macOS code signing certificates. For Snap, one can try to submit the app to a snap store so it can be installed with a GUI.

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
