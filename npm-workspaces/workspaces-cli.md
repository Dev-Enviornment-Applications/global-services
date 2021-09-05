# NPM Workspaces - https://docs.npmjs.com/cli/v7/using-npm/workspaces
## Table of Contents
https://dev.to/limal/simplify-your-monorepo-with-npm-7-workspaces-5gmj
https://dev.to/ruyadorno/npm-workspaces-npm-run-and-exec-1lg0

[Getting started with workspaces](#Getting-started-with-workspaces)
[Adding dependencies to a workspace](#Adding-dependencies-to-a-workspace)
[Using workspaces](#Using-workspaces)
[Running commands in the context of workspaces](#Running-commands-in-the-context-of-workspaces)

## Getting started with workspaces
You may automate the required steps to define a new workspace using npm init. For example in a project that already has a package.json defined you can run:

> npm init -w ./packages/a

This command will create the missing folders and a new package.json file (if needed) while also making sure to properly configure the "workspaces" property of your root project package.json.
--------------------------------------------------------------------
--------------------------------------------------------------------
## Adding dependencies to a workspace
It's possible to directly add/remove/update dependencies of your workspaces using the workspace config.
For example, assuming the following structure:

.
+-- package.json
`-- packages
   +-- a
   |   `-- package.json
   `-- b
       `-- package.json

If you want to add a dependency named <abbrev> from the registry as a dependency of your workspace a, you may use the workspace config to tell the npm installer that package should be added as a dependency of the provided workspace:

> npm install abbrev -w a

Note: other installing commands such as uninstall, ci, etc will also respect the provided workspace configuration.
--------------------------------------------------------------------
--------------------------------------------------------------------
## Using workspaces
Given the specifities of how Node.js handles module resolution it's possible to consume any defined workspace by it's declared package.json name. Continuing from the example defined above, let's also create a Node.js script that will require the workspace-a example module, e.g:

// ./workspace-a/index.js
module.exports = 'a'

// ./lib/index.js
const moduleA = require('workspace-a')
console.log(moduleA) // -> a

When running it with:

> node lib/index.js

This demonstrates how the nature of node_modules resolution allows for workspaces to enable a portable workflow for requiring each workspace in such a way that is also easy to publish these nested workspaces to be consumed elsewhere.
--------------------------------------------------------------------
--------------------------------------------------------------------
## Running commands in the context of workspaces
You can use the workspace configuration option to run commands in the context of a configured workspace.
Following is a quick example on how to use the npm run command in the context of nested workspaces. For a project containing multiple workspaces, e.g:

.
+-- package.json
`-- packages
   +-- a
   |   `-- package.json
   `-- b
       `-- package.json

By running a command using the workspace option, it's possible to run the given command in the context of that specific workspace. e.g:

> npm run test --workspace=a

This will run the test script defined within the ./packages/a/package.json file.
Please note that you can also specify this argument multiple times in the command-line in order to target multiple workspaces, e.g:

> npm run test --workspace=a --workspace=b

It's also possible to use the workspaces (plural) configuration option to enable the same behavior but running that command in the context of all configured workspaces. e.g:

> npm run test --workspaces

Will run the test script in both ./packages/a and ./packages/b.
--------------------------------------------------------------------
--------------------------------------------------------------------