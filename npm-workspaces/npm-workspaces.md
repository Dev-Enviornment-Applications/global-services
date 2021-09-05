
### [](#description)Description 
**Workspaces** is a generic term that refers to the set of features in the npm cli that provides support to managing multiple packages from your local files system from within a singular top-level, root package. This set of features makes up for a much more streamlined workflow handling linked packages from the local file system. Automating the linking process as part of `npm install` and avoiding manually having to use `npm link` in order to add references to packages that should be symlinked into the current `node_modules` folder. We also refer to these packages being auto-symlinked during `npm install` as a single **workspace**, meaning it's a nested package within the current local file system that is explicitly defined in the [`package.json`](/cli/v7/configuring-npm/package-json#workspaces) `workspaces` configuration. ### [](#defining-workspaces)Defining workspaces Workspaces are usually defined via the `workspaces` property of the [`package.json`](/cli/v7/configuring-npm/package-json#workspaces) file, e.g:

<div class="Box-sc-1b6inku-0 Position-gj4o9g-0 dIAadT">

<pre class="
                        Box-sc-1b6inku-0
                        BorderBox-sc-1y9cbfx-0
                        jRndWL
                        prism-code
                        language-json
                      " style="
                        color: #393a34;
                        background-color: #f6f8fa;
                        overflow: auto;
                      ">

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token punctuation" style="color:#393A34">{</span><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain"></span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain"></span> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token property" style="color:#36acaa">"name"</span><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token operator" style="color:#393A34">:</span> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain"></span> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token string" style="color:#e3116c">"my-workspaces-powered-project"</span><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token punctuation" style="color:#393A34">,</span><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain"></span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain"></span> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token property" style="color:#36acaa">"workspaces"</span><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token operator" style="color:#393A34">:</span> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain"></span> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token punctuation" style="color:#393A34">[</span><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain"></span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain"></span> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token string" style="color:#e3116c">"workspace-a"</span><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain"></span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain"></span> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token punctuation" style="color:#393A34">]</span><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain"></span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain"></span><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token punctuation" style="color:#393A34">}</span></div>

</pre>

</div>

Given the above `package.json` example living at a current working directory `.` that contains a folder named `workspace-a` that itself contains a `package.json` inside it, defining a Node.js package, e.g:

<div class="Box-sc-1b6inku-0 Position-gj4o9g-0 dIAadT">

<pre class="
                        Box-sc-1b6inku-0
                        BorderBox-sc-1y9cbfx-0
                        jRndWL
                        prism-code
                        language-
                      " style="
                        color: #393a34;
                        background-color: #f6f8fa;
                        overflow: auto;
                      ">

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">.</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">+-- package.json</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">`-- workspace-a</span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">`-- package.json</span></div>

</pre>

</div>

The expected result once running `npm install` in this current working directory `.` is that the folder `workspace-a` will get symlinked to the `node_modules` folder of the current working dir. Below is a post `npm install` example, given that same previous example structure of files and folders:

<div class="Box-sc-1b6inku-0 Position-gj4o9g-0 dIAadT">

<pre class="
                        Box-sc-1b6inku-0
                        BorderBox-sc-1y9cbfx-0
                        jRndWL
                        prism-code
                        language-
                      " style="
                        color: #393a34;
                        background-color: #f6f8fa;
                        overflow: auto;
                      ">

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">.</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">+-- node_modules</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">|  `-- workspace-a -> ../workspace-a</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">+-- package-lock.json</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">+-- package.json</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">`-- workspace-a</span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">`-- package.json</span></div>

</pre>

</div>

### [](#getting-started-with-workspaces)Getting started with workspaces You may automate the required steps to define a new workspace using [npm init](/cli/v7/commands/npm-init). For example in a project that already has a `package.json` defined you can run:

<div class="Box-sc-1b6inku-0 Position-gj4o9g-0 dIAadT">

<pre class="
                        Box-sc-1b6inku-0
                        BorderBox-sc-1y9cbfx-0
                        jRndWL
                        prism-code
                        language-
                      " style="
                        color: #393a34;
                        background-color: #f6f8fa;
                        overflow: auto;
                      ">

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">npm init -w ./packages/a</span></div>

</pre>

</div>

This command will create the missing folders and a new `package.json` file (if needed) while also making sure to properly configure the `"workspaces"` property of your root project `package.json`. ### [](#adding-dependencies-to-a-workspace)Adding dependencies to a workspace It's possible to directly add/remove/update dependencies of your workspaces using the [`workspace` config](/cli/v7/using-npm/config#workspace). For example, assuming the following structure:

<div class="Box-sc-1b6inku-0 Position-gj4o9g-0 dIAadT">

<pre class="
                        Box-sc-1b6inku-0
                        BorderBox-sc-1y9cbfx-0
                        jRndWL
                        prism-code
                        language-
                      " style="
                        color: #393a34;
                        background-color: #f6f8fa;
                        overflow: auto;
                      ">

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">.</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">+-- package.json</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">`-- packages</span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">+-- a</span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">|   `-- package.json</span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">`-- b</span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">`-- package.json</span></div>

</pre>

</div>

If you want to add a dependency named `abbrev` from the registry as a dependency of your workspace **a**, you may use the workspace config to tell the npm installer that package should be added as a dependency of the provided workspace:

<div class="Box-sc-1b6inku-0 Position-gj4o9g-0 dIAadT">

<pre class="
                        Box-sc-1b6inku-0
                        BorderBox-sc-1y9cbfx-0
                        jRndWL
                        prism-code
                        language-
                      " style="
                        color: #393a34;
                        background-color: #f6f8fa;
                        overflow: auto;
                      ">

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">npm install abbrev -w a</span></div>

</pre>

</div>

Note: other installing commands such as `uninstall`, `ci`, etc will also respect the provided `workspace` configuration. ### [](#using-workspaces)Using workspaces Given the [specifities of how Node.js handles module resolution](https://nodejs.org/dist/latest-v14.x/docs/api/modules.html#modules_all_together) it's possible to consume any defined workspace by it's declared `package.json` `name`. Continuing from the example defined above, let's also create a Node.js script that will require the `workspace-a` example module, e.g:

<div class="Box-sc-1b6inku-0 Position-gj4o9g-0 dIAadT">

<pre class="
                        Box-sc-1b6inku-0
                        BorderBox-sc-1y9cbfx-0
                        jRndWL
                        prism-code
                        language-
                      " style="
                        color: #393a34;
                        background-color: #f6f8fa;
                        overflow: auto;
                      ">

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">// ./workspace-a/index.js</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">module.exports = 'a'</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain" style="display:inline-block"></span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">// ./lib/index.js</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">const moduleA = require('workspace-a')</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">console.log(moduleA) // -> a</span></div>

</pre>

</div>

When running it with: `node lib/index.js` This demonstrates how the nature of `node_modules` resolution allows for **workspaces** to enable a portable workflow for requiring each **workspace** in such a way that is also easy to [publish](/cli/v7/commands/npm-publish) these nested workspaces to be consumed elsewhere. ### [](#running-commands-in-the-context-of-workspaces)Running commands in the context of workspaces You can use the `workspace` configuration option to run commands in the context of a configured workspace. Following is a quick example on how to use the `npm run` command in the context of nested workspaces. For a project containing multiple workspaces, e.g:

<div class="Box-sc-1b6inku-0 Position-gj4o9g-0 dIAadT">

<pre class="
                        Box-sc-1b6inku-0
                        BorderBox-sc-1y9cbfx-0
                        jRndWL
                        prism-code
                        language-
                      " style="
                        color: #393a34;
                        background-color: #f6f8fa;
                        overflow: auto;
                      ">

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">.</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">+-- package.json</span></div>

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">`-- packages</span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">+-- a</span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">|   `-- package.json</span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">`-- b</span></div>

<div class="token-line" style="color:#393A34"> <span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">`-- package.json</span></div>

</pre>

</div>

By running a command using the `workspace` option, it's possible to run the given command in the context of that specific workspace. e.g:

<div class="Box-sc-1b6inku-0 Position-gj4o9g-0 dIAadT">

<pre class="
                        Box-sc-1b6inku-0
                        BorderBox-sc-1y9cbfx-0
                        jRndWL
                        prism-code
                        language-
                      " style="
                        color: #393a34;
                        background-color: #f6f8fa;
                        overflow: auto;
                      ">

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">npm run test --workspace=a</span></div>

</pre>

</div>

This will run the `test` script defined within the `./packages/a/package.json` file. Please note that you can also specify this argument multiple times in the command-line in order to target multiple workspaces, e.g:

<div class="Box-sc-1b6inku-0 Position-gj4o9g-0 dIAadT">

<pre class="
                        Box-sc-1b6inku-0
                        BorderBox-sc-1y9cbfx-0
                        jRndWL
                        prism-code
                        language-
                      " style="
                        color: #393a34;
                        background-color: #f6f8fa;
                        overflow: auto;
                      ">

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">npm run test --workspace=a --workspace=b</span></div>

</pre>

</div>

It's also possible to use the `workspaces` (plural) configuration option to enable the same behavior but running that command in the context of **all** configured workspaces. e.g:

<div class="Box-sc-1b6inku-0 Position-gj4o9g-0 dIAadT">

<pre class="
                        Box-sc-1b6inku-0
                        BorderBox-sc-1y9cbfx-0
                        jRndWL
                        prism-code
                        language-
                      " style="
                        color: #393a34;
                        background-color: #f6f8fa;
                        overflow: auto;
                      ">

<div class="token-line" style="color:#393A34"><span font-family="mono" font-size="1" class="Text-sc-1g6etse-0 bbMPSg token plain">npm run test --workspaces</span></div>

</pre>

</div>

Will run the `test` script in both `./packages/a` and `./packages/b`. 
### [](#see-also)See also * [npm install](https://docs.npmjs.com/cli/v7/commands/npm-install) * [npm publish](https://docs.npmjs.com/cli/v7/commands/npm-publish) * [npm run-script](https://docs.npmjs.com/cli/v7/commands/npm-run-script) * [config](https://docs.npmjs.com/cli/v7/using-npm/config)</div>

