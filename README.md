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
- Can you run `install` from within the root?
- How are the packages installed in `node_modules`? (symlink, flat?)

#### Running a single script in all workspaces
- Serially
- In parallel, with streaming output

#### Filtering workspaces
- Include
- Exclude

#### Updating dependencies across the repo
- Does the tooling allow for updating lodash in both workspaces?
- Does it allow for updating to the same version in both?
- Does it sync the package.json files?
