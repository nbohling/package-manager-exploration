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
  - Yes, from file:
  - From root: `npm install --save --workspace=@nb/package2 ./workspaces/package1`
  - From package2 dir: `npm install ../package1`
- Can you run `install` from within the root?
  - Yes, no problems.
- How are the packages installed in `node_modules`? (symlink, flat?)
  - package.json is updated with name and dir
  - package is symlinked in package2's node_modules dir
  - Both workspaces/packages are symlinked from the top-level node_modules

#### Running a single script in all workspaces
- Serially
  - `npm run go-once --workspaces`
- In parallel, with streaming output
  - not possible

#### Filtering workspaces
- Include
  - `npm run go-once -w @nb/package1 -w @nb/package2`
- Exclude
  - not possible, just selecting one at a time

#### Updating dependencies across the repo
- Does the tooling allow for updating lodash in both workspaces?
  - `npm update --workspaces` will update all versions
- Does it allow for updating to the same version in both?
  - Sort of -- `npm install lodash@latest --save --workspaces` will re-install latest in all workspaces
- Does it sync the package.json files?
  - Yes, `npm install lodash@latest --save --workspaces` saves to package.json

#### Other notes:
There's a bug in npm that doesn't handle including dependencies in subdirectories very well.
https://github.com/npm/cli/issues/3847

