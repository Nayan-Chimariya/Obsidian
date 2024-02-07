#### What is Node?
Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It is not a library or a framework, it is a platform that allows developers to run JavaScript on the server-side.

#### Get node

Download Node from [here](https://nodejs.org/en/download/)
Get `LTS (Long term support)` for development and `current` for testing features

#### Check for installation
Open the terminal and run these commands to check for the version of Node and nmp on your machine:

```bash
node --version
nmp --version
```
These commands should result in this output
![[node installation.png]]

#### What is NPM?
NPM is a package manager for Node.js packages
#### Running js files using node
Use the node command in the terminal followed by the js file name (extension is optional as node is intended to run js file only)

```node
node test.js
```
OR
```node
node test
```

#### Creating node package
- What is a node package?
	A package in Node.js contains all the files you need for a module.
	Modules are JavaScript libraries you can include in your project.
- Command to initialize:
```node
nmp init
```
This will create a file `package.json` that has the following example content which can be customized at the phase of initializing 

```json
{

"name": "tutorial",

"version": "1.0.0",

"description": "",

"main": "hello.js",

"scripts": {

"test": "echo \"Error: no test specified\" && exit 1",

"start": "node hello.js"

},

"author": "nayan",

"license": "ISC"

}
```
