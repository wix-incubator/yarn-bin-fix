# yarn node_modules/.bin/ fix
Fix for yarn's [#760](https://github.com/yarnpkg/yarn/issues/760)

This does exactly what npm usually does, links all package.json's `bin` executables into the top-most `node_modules/.bin` (recursively). 

Currently, yarn does not do that. So if you have transitive dependencies (dependency of dependency) that has an executable, you will not be able to run it if installing with yarn.

For example, you depend on `standard` which depend on `eslint`. When using npm, you could just run `eslint src` and everything worked. With yarn this will not work.

This is not a perfect solution, but this script will allow you to migrate to yarn more easily. See (#1210)(https://github.com/yarnpkg/yarn/pull/1210).

## Installation
Install it globally (for ease of access, not necessary).

`npm i -g yarn-bin-fix`

## Usage
After installing your module using `yarn`, run `yarn-bin-fix` from your **project's root**.

Keep in mind that if you have `postinstall` scripts that use transitive dependencies, these will fail until you run this script.
