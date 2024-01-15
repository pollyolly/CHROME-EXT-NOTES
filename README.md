## CHROME-EXT-NOTES

### Installation
```
a. Go to Chrome Extensions
b. Click Chrome manage Extension
c. Click extensions Developer Mode
d. Click extensions Load Unpacked
e. Upload your Extension project folder
f. Click in upper-right corner the Chrome Extension Icon
g. Click pin extension
```
### Structure

<img src="https://github.com/pollyolly/CHROME-EXT-NOTES/blob/main/extension-structure.png" width="150"/>

### Manifest
manifest.json
```json
{
    "manifest_version": 3,
    "name": "PDF Text Reader",
    "description": "PDF Text Reader Chrome Extension",
    "version": "1.0.0",
    "action": {
        "default_popup": "window.html",
        "default_logo": "icon16.png"
    },
    "icons": {
        "16": "icons/icon16.png",
        "32": "icons/icon32.png",
        "48": "icons/icon48.png",
        "128": "icons/icon128.png"
      },
    "background": {
        "service_worker": "background.js"
    },
    "permissions": ["activeTab", "scripting"],
    "commands": {
        "_execute_action": {
            "suggested_key": {
                "default": "Ctrl+B",
                "mac": "Command+B"
            }
        }
    }
}

```
### Package JSON
```
$ cd pdf-ireader/
$ npm init
$ npm install react
$ npm install react-dom
$ npm install webpack
$ npm install webpack-cli
```
package.json
```
{
  "name": "pdf-ireader",
  "version": "1.0.0",
  "description": "[Chrome Ext Generator](https://alexleybourne.github.io/chrome-extension-icon-generator/)",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "webpack": "^5.89.0",
    "webpack-cli": "^5.1.4"
  }
}
```
### Reference
[Google Extension](https://developer.chrome.com/docs/extensions/get-started/tutorial/hello-world)
