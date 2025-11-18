# Jumbo

Jumbo is a Julia distribution that comes with commonly needed scientific packages out of the box. Start using Makie, DifferentialEquations, or any included package immediately - no compilation wait. Additional packages can be installed via Pkg without triggering recompilation of pre-installed packages.

This repository also serves as a template for creating custom Julia distributions tailored to your needs. Fork it, modify the `Project.toml` to include your preferred packages, and run the "Build Release Assets" GitHub Actions workflow to generate installers for Linux, macOS, and Windows. The distribution format uses a `Project.toml` with `name` and `version` fields - bundling all listed packages and dependencies into the stdlib path to prevent accidental recompilations.

## Installation

To install Jumbo, download the appropriate pre-built distribution (MSIX, Snap, or DMG) from the **Assets** section on the [releases page](https://github.com/JanisErdmanis/JuBox/releases) (you may need to expand the Assets dropdown for prerelease versions), then follow the installation instructions below for your platform:

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
