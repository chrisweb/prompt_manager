---
mode: 'agent'
---

before you start, first read the [environment prompt](environment.prompt.md) content
when editing files make sure to follow the [editorconfig](../../.editorconfig) settings

edit the package.json (in the root of the project):

* make sure all packages use an exact version and make sure the latest version of each package is being used
* to check what the latest version of a package is, you can use the command `npm view <package-name> version`, chain the commands to make the process faster
* to see the installed packages and their versions, you can read the content of the package.json file or use the command `npm list --depth=0`
* when the package.json update is done, make sure you save the file
* after saving the file run the `npm i` command to update the dependencies