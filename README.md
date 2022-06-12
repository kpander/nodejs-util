# nodejs-util

This is a static class of common helper methods, for use in NodeJS code.

## Installation

Ensure your project has a `.npmrc` file in the project root to tell `npm` where to find the package. Ensure the following line exists:
```
@kpander:registry=https://npm.pkg.github.com/
```

Then:
```
$ npm install @kpander/nodejs-util
```

## Methods

### &lt;array&gt; getFiles(&lt;string&gt; folder)

Recursively get all files in the given `folder`. Always returns an array of strings unless an invalid/non-existent `folder` is specified in which case boolean `false` is returned.

```js
const Util = require("@kpander/nodejs-util");
const files = Util.getFiles("/path/to/my/files");
console.log(files);
```
```
[
  "/path/to/my/files/file1.txt",
  "/path/to/my/files/file2.txt",
  "/path/to/my/files/subfolder1/some-file1.txt",
  "/path/to/my/files/subfolder2/some-file2.txt",
]
```

### &lt;boolean&gt; ensureFolder(&lt;string&gt; folder)

Create the given `folder` if it doesn't already exist (along with any needed parent folders). Always returns `true` unless an empty or non-string `folder` is specified.

```js
const Util = require("@kpander/nodejs-util");
Util.ensureFolder("/path/to/my/new/folder");
```

### &lt;boolean&gt; hasProp(&lt;object&gt; obj, &lt;string&gt; key)

Returns `true` if the given `key` exists in the given `obj`.

```js
const Util = require("@kpander/nodejs-util");
const obj = { key1: "key1", key2: "key2" };
console.log("key1 exists in obj:", Util.hasProp(obj, "key1"));
console.log("key99 exists in obj:", Util.hasProp(obj, "key99"));
```
```
key1 exists in obj: true
key99 exists in obj: false
```

### &lt;string&gt; replaceAll(&lt;string&gt; content, &lt;string&gt; search, &lt;string&gt; replace)

Replace all instances of `search` with `replace`, in the given `content`.

```js
const Util = require("@kpander/nodejs-util");
const content = `
I had a chicken.
The chicken liked pizza.
But not if the pizza had chicken on it.
`.trim();
const search = "chicken";
const replace = "turkey";

const result = Util.replaceAll(content, search, replace);
console.log("Original:", content);
console.log("Replaced:", replace);
```
```
Original: I had a chicken.
The chicken liked pizza.
But not if the pizza had chicken on it.

Replaced: I had a turkey.
The turkey liked pizza.
But not if the pizza had turkey on it.
```

### &lt;boolean&gt; touch(&lt;string&gt; filename)

If `filename` doesn't already exist, create it as a 0-byte empty file. **Containing folders will be created if needed.** If `filename` already exists, do nothing. Returns `true` unless the given `filename` is not a string.

```js
const fs = require("fs");
const Util = require("@kpander/nodejs-util");
Util.touch("/path/to/empty-file.txt");

console.log("Empty file:", fs.readFileSync("/path/to/empty-file.txt", "utf8"));
```
```
Empty file:
```

## Maintainer

- Kendall Anderson (kpander@invisiblethreads.com)

