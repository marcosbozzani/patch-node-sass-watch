# patch-node-sass-watch

## Overview

This patch is just a temporary solution for 'File to read not found or unreadable' and 'File to import not found or unreadable' errors that occasionally happens after a file save in Visual Studio Code when node-sass is running on watch mode. Those errors happen with 'node-sass (watch mode)', 'chokidar + node-sass' and 'node-sass-chokidar (watch mode)'.

The patch is applied to [lib/render.js](lib/render.js), you can just search for `_patch_*` function and variables.

If those errors are detected, a retry mechanism is applied. It verifies that the file actually exists and limits the maximum number of retries. The retry limit is there as a safety measure to prevent infinite recursion and the value is high enough for those cases where the machine is really slow or it has to access a storage with high latency.

## Setup

1. Create a folder named `patches` in your project 
2. Download the [patch](patches/node-sass+4.14.1.patch) to your project `patches` folder
3. Install `patch-package`
   - In package.json
   ```
   "scripts": {
     "postinstall": "patch-package"
   }
   ```
   - if you use *npm*
   ```
   npm i patch-package
   ```
   - if you use *yarn*
   ```
   yarn add patch-package postinstall-postinstall
   ```

## Related issues:

https://github.com/sass/node-sass/issues/1894

https://github.com/sass/node-sass/issues/2022

https://github.com/microsoft/vscode/issues/20491

https://github.com/facebook/create-react-app/issues/2531

https://github.com/michaelwayman/node-sass-chokidar/issues/14

https://github.com/michaelwayman/node-sass-chokidar/issues/22

https://stackoverflow.com/questions/50395998/vscode-wont-work-with-filewatchers

