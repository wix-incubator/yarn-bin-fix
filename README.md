# yarn-link and npm-link node_modules/.bin/ fix

`npm install my-package`/`yarn add my-package` usually links all my-package' dependencies' `bin` executables into the top-most `node_modules/.bin` (recursively). 

Currently, both `npm link my-package` / `yarn link my-package` and `npm install folder` don't do that. So if you have transitive dependencies (dependency of dependency) that has an executable, you will not be able to run it if linking with yarn/npm.

For example, you depend on `standard` which depend on `eslint`. When using `npm install`, you could just run `eslint src` and everything worked. With `npm link standard` this will not work.

## Installation
Install it globally (for ease of access, not necessary).

`npm i -g yarn-bin-fix`

## Usage
After linking your module using `npm link my-package` or `yarn link my-package`, run `yarn-bin-fix` from your **project's root**.

Keep in mind that if you have `postinstall` scripts that use transitive dependencies, these will fail until you run this script.
