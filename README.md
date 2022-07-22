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
  - `yarn add file:workspaces/package1` from package2 dir works
  - You can also add the dependency to package.json manually (`@nb/package1": "^1.0.0",`), and it links automatically on yarn install.
- Can you run `install` from within the root?
  - Yes
- How are the packages installed in `node_modules`? (symlink, flat?)
  - Symlinks

#### Running a single script in all workspaces
- Serially
  - `yarn workspaces run go-once`
- In parallel, with streaming output
  - Not supported, need to use something like concurrency

#### Filtering workspaces
- Include
  - Can select once at a time, but not multiple
- Exclude
  - Not supported

#### Updating dependencies across the repo
- Does the tooling allow for updating lodash in both workspaces?
  - `yarn upgrade lodash --latest` to stay within defined versions
  - `yarn upgrade-interactive --latest` to update package.json
- Does it allow for updating to the same version in both?
  - `yarn upgrade-interactive --latest` can do it
- Does it sync the package.json files?
  - `yarn upgrade-interactive --latest` will save
