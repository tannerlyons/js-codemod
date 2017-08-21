# js-codemods [![Build Status](https://travis-ci.org/tannermeans/js-codemod.svg)](https://travis-ci.org/tannermeans/js-codemod)

These scripts are all written for use with Facebook's jscodeshift:
[https://github.com/facebook/jscodeshift](https://github.com/facebook/jscodeshift)

### Prerequisites

```sh
npm install -g jscodeshift
git clone https://github.com/tannermeans/js-codemod.git
jscodeshift -t transforms/<codemod>.js <js file to transform>
```

### Transform summary:

#### object-create-to-class.js

```sh
jscodeshift -t js-codemod/transform/object-create-to-class.js <js file to transform>
```

### Tips:
An easy way to set up your transforms is with a wrapper script like this:
```js
#!/usr/bin/node

const execSync = require("child_process").execSync;

// Assuming you call this script like: `node wrapper.js InputFile.js`
const inputFile = process.argv[2];

const pipeline = [
  "js-codemod/transform/object-create-to-class.js",
  "transform-2.js"
];

pipeline.forEach(stepPath => {
  execSync(`jscodeshift -t ${stepPath} ${inputFile}`);
});

console.log("DONE");
```