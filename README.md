Application example for Kitu suite, style of tiny third person style shooter, works as starter project.

-----

## Dependencies

see `manifest.json`. no need purchasing extra assets.

-----

# Breakdown

## Strategy of manage source / version control

- Git LFS
- `My-app-front` (`***-front`) is Unity project (build from URP Core template). designing concept is based on Kitu-Headless.

### Art, asset resource management

avoid doubling art resource in this repository, e.g. whole exported .fbx files.

## CI/CD, build targets, Testing workflow


## Unity frontend project (My-app-front)

- Kitu frontend interface sources
- folder(directory) structure
- multi scene editing


## BFF (Backend For Frontend) project

prototyping note

- .NET 7.0 install
- following MagicOnion Quick Start https://github.com/Cysharp/MagicOnion#quick-start
    - `dotnet new web -o My-app-BFF`
