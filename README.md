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
### Project Structure
```vim
pdf-ireader-ext/
---icons/
------icon16.png
------icon32.png
------icon148.png
------icon128.png
---popup/
------popup.css
------popup.js
---scripts/
------content.js
---background.js
---index.js
---manifest.json
---pdf-ireader.css
---window.html
---icon16.png
---webpack.config.js
---tsconfig.json
```
### Manifest JSON
pdf-ireader-ext/manifest.json (Create Manually)
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
package.json (Automatically Created)
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
### TSConfig
```
$ cd pdf-ireader-ext/
$ npm install ts-loader
```
tsconfig.json (Create Manually)
```
{
    "compilerOptions": {
        "jsx": "react",
        "module": "es6",
        "target": "es6",
        "moduleResolution": "node",
        "esModuleInterop": true,
    },
    "include": ["src/**/*.ts", "src/**/*.tsx"],
    "exclude": ["node_modules"],
}{
    "compilerOptions": {
        "jsx": "react",
        "module": "es6",
        "target": "es6",
        "moduleResolution": "node",
        "esModuleInterop": true,
    },
    "include": ["src/**/*.ts", "src/**/*.tsx"],
    "exclude": ["node_modules"],
}
```
### Webpack 5
webpack.config.js (Create Manually)
```
module.exports = {
    mode: "development",
    entry: "./src/test.tsx",
    module: {
        rules: [{
            use: "ts-loader",
            test: /\.tsx$/,
            exclude: /node_modules/
    }]
    },
    resolve: {
        extensions: ['.tsx', '.ts', '.js']
    },
    output: {
        filename: "index.js"
    }
}
```
```
$ cd pdf-ireader-ext/
$ npm run dev
```
Compiled generated
```
pdf-ireader-ext/dist/index.js
```
### Manifest.json and Package JSON
```
scripts: { "watch": "webpack --watch --progress --config webpack.config.js" }
```
Added in package.json 
```
{
  "name": "pdf-ireader",
  "version": "1.0.0",
  "description": "[Chrome Ext Generator](https://alexleybourne.github.io/chrome-extension-icon-generator/)",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "webpack",
    "watch": "webpack --watch --progress --config webpack.config.js"
  },
  "author": "",
  "license": "MIT",
  "dependencies": {
    "copy-webpack-plugin": "^12.0.1",
    "path": "^0.12.7",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "ts-loader": "^9.5.1",
    "webpack": "^5.89.0",
    "webpack-cli": "^5.1.4"
  }
}

```
```
$ npm install copy-webpack-plugin
$ npm install path
$ npm install html-webpack-plugin
```
```
const path = require('path');
const CopyPlugin = require('copy-webpack-plugin');
const HtmlPlugin = require('html-webpack-plugin');

module.exports = {
    mode: "development",
    entry: "./src/test.tsx",
    module: {
        rules:[
        {
            use: "ts-loader",
            test: /\.tsx$/,
            exclude: /node_modules/
        },
//    get resources
        {
            type: "assets/resource",
            use: 'assets/resource',
            test: /\.(png|jpg|jpeg|gif|woff|tff|eot|svg)$/,
        },
    ]
    },
    plugins: [
        new CopyPlugin({
            patterns: [
                {
                    from: path.resolve("manifest.json"),
                    to: path.resolve("dist/")
                }
            ]
        }),
        ...getHmlPlugins(['popup', options]) //Get Chunks dynamically
    ],
    resolve: {
        extensions: ['.tsx', '.ts', '.js']
    },
    output: {
        filename: '[name].js'  //get name on Chunks
    },
    
}
//Automatically iterate on Chunks
function getHtmlPlugins(chunks){
    return chunks.map(chunk => new HtmlPlugin({
        title: 'PDF iReader Ext',
        filename: `${chunk}.html`,
        chunks: [chunks]
    }));
}
```
```
$ npm run watch
```
### Reference
[Google Extension](https://developer.chrome.com/docs/extensions/get-started/tutorial/hello-world)

[Webpack 5](https://webpack.js.org/concepts/plugins/)
