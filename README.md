# package-manager-exploration
Exploring package managers

## Purpose
This repository is built to explore using various package managers.

We'll use a new branch to explore each package manager (npm, yarn, yarn2, pnpm), so use the `branch` selector above to switch between them.

## Structure
It contains two workspaces:
- workspaces/@nb/package1
- workspaces/@nb/package2

Each package has a dependency on a different version of lodash.

Package2 depends on Package1 in order to create some internal dependencies.

## Running
Each subapp contains a "go" script that repeatedly emits output.

## Tests

#### Automatically linking other packages from the same repo
- Can you add package1 as a dependency to package2?
  - `pnpm add @nb/package1` works perfectly
- Can you run `install` from within the root?
  - of course
- How are the packages installed in `node_modules`? (symlink, flat?)
  - Symlinked together

#### Running a single script in all workspaces
- Serially
  - `pnpm run --recursive go-once`
- In parallel, with streaming output
  - `pnpm run --recursive --parallel --stream go-repeatedly`

#### Filtering workspaces
- Include
  - `--filter=@nb/*`
- Exclude
  - `--filter=!@nb/*`

#### Updating dependencies across the repo
- Does the tooling allow for updating lodash in both workspaces?
  - `pnpm up -r -L`
- Does it allow for updating to the same version in both?
  - Yes, `pnpm up -r -L`
- Does it sync the package.json files?
  - `pnpm up -r -L` updates to newest version and updates packages.json
