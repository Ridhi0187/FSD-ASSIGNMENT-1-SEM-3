# Node.js Module Caching

## Full Stack Development Assignment

### 1. Aim

To understand Node.js module caching and demonstrate how multiple JavaScript files can share the same exported object using `require()`.

### 2. Introduction

Node.js uses module caching to avoid loading and executing the same resolved module repeatedly. When a module is loaded for the first time, Node.js stores its exports in the module cache. Subsequent `require()` calls for that module return the cached exports.

### 3. Technologies Used

* Node.js
* JavaScript
* Visual Studio Code

### 4. Project Structure

* `shared.js` — Creates and exports a shared object.
* `file1.js` — Imports the shared object and increments its counter.
* `file2.js` — Imports the same object and increments its counter again.
* `app.js` — Runs both files in the same Node.js process.

### 5. Implementation

**shared.js**

```javascript
const sharedObject = {
    count: 0
};

module.exports = sharedObject;
```

**file1.js**

```javascript
const shared = require('./shared');

shared.count += 1;

console.log("File 1 count:", shared.count);
```

**file2.js**

```javascript
const shared = require('./shared');

shared.count += 1;

console.log("File 2 count:", shared.count);
```

**app.js**

```javascript
require('./file1');
require('./file2');
```

### 6. Execution

Run the following command in the VS Code terminal:

```bash
node app.js
```

### 7. Output

```text
File 1 count: 1
File 2 count: 2
```

### 8. Explanation

First, `file1.js` imports the shared object and increments its counter from 0 to 1. Node.js caches the exports of `shared.js`. Next, `file2.js` imports the same cached object and increments the counter from 1 to 2.

Both files run in the same Node.js process, so they access the same exported object.

### 9. Conclusion

Node.js module caching improves performance by reusing cached module exports. This example demonstrates that multiple files can access and modify the same exported object through `require()`.

**Note:** This demonstration uses a custom module to illustrate caching. Node.js also caches CommonJS modules according to their resolved module identity, with special handling for built-in modules.
