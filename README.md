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
  - `yarn add @nb/package1` works great.
- Can you run `install` from within the root?
  - Yes
- How are the packages installed in `node_modules`? (symlink, flat?)
  - symlink only at the top level

#### Running a single script in all workspaces

- Serially
  - `yarn workspaces foreach run go-once`
- In parallel, with streaming output
  - `yarn workspaces foreach run --parallel --interlaced go-repeatedly`

#### Filtering workspaces

- Include
  - `--include` by indents
  - `yarn workspaces foreach --include "@nb/package*" run go-once`
- Exclude
  - `--exclude`

#### Updating dependencies across the repo

- Does the tooling allow for updating lodash in both workspaces?
  - `yarn up lodash@latest`
- Does it allow for updating to the same version in both?
  - Yes, - `yarn up lodash@latest` updates everything to `latest`
- Does it sync the package.json files?
  - Yes - `yarn up lodash@latest` saves in package.json
