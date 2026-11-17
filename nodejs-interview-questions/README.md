[⬅ Back](../README.md)

[⬅ Return to Root README](../README.md)

# Node.js Interview Questions & Answers

> Click :star: if you like the project. Pull Request are highly appreciated.

### Table of Contents

| No. | Questions |
|---- | ---------
|1  | [What is Node.js?](#what-is-nodejs) |
|2  | [What are the key features of Node.js?](#what-are-the-key-features-of-nodejs) |
|3  | [What is the difference between Node.js and JavaScript?](#what-is-the-difference-between-nodejs-and-javascript) |
|4  | [What is the V8 engine?](#what-is-the-v8-engine) |
|5  | [What is Event Loop in Node.js?](#what-is-event-loop-in-nodejs) |
|6  | [What is the purpose of module.exports?](#what-is-the-purpose-of-moduleexports) |
|7  | [What is the difference between require() and import?](#what-is-the-difference-between-require-and-import) |
|8  | [What is npm?](#what-is-npm) |
|9  | [What is package.json?](#what-is-packagejson) |
|10 | [What is the difference between dependencies and devDependencies?](#what-is-the-difference-between-dependencies-and-devdependencies) |
|11 | [What is callback in Node.js?](#what-is-callback-in-nodejs) |
|12 | [What is callback hell?](#what-is-callback-hell) |
|13 | [How do you prevent callback hell?](#how-do-you-prevent-callback-hell) |
|14 | [What are Promises in Node.js?](#what-are-promises-in-nodejs) |
|15 | [What is async/await?](#what-is-asyncawait) |
|16 | [What is the difference between synchronous and asynchronous functions?](#what-is-the-difference-between-synchronous-and-asynchronous-functions) |
|17 | [What are Streams in Node.js?](#what-are-streams-in-nodejs) |
|18 | [What are the types of Streams?](#what-are-the-types-of-streams) |
|19 | [What is Buffer in Node.js?](#what-is-buffer-in-nodejs) |
|20 | [What is middleware in Express.js?](#what-is-middleware-in-expressjs) |
|21 | [What is the purpose of next() in middleware?](#what-is-the-purpose-of-next-in-middleware) |
|22 | [What is the difference between process.nextTick() and setImmediate()?](#what-is-the-difference-between-processnexttick-and-setimmediate) |
|23 | [What is Event Emitter?](#what-is-event-emitter) |
|24 | [What is the purpose of the cluster module?](#what-is-the-purpose-of-the-cluster-module) |
|25 | [What is the difference between fork() and spawn()?](#what-is-the-difference-between-fork-and-spawn) |
|26 | [What is REPL in Node.js?](#what-is-repl-in-nodejs) |
|27 | [What is the purpose of the crypto module?](#what-is-the-purpose-of-the-crypto-module) |
|28 | [What is the difference between readFile and createReadStream?](#what-is-the-difference-between-readfile-and-createreadstream) |
|29 | [How do you handle errors in Node.js?](#how-do-you-handle-errors-in-nodejs) |
|30 | [What is global object in Node.js?](#what-is-global-object-in-nodejs) |
|31 | [What is the purpose of __dirname and __filename?](#what-is-the-purpose-of-__dirname-and-__filename) |
|32 | [What is the difference between req.params, req.query and req.body?](#what-is-the-difference-between-reqparams-reqquery-and-reqbody) |
|33 | [What is cors in Node.js?](#what-is-cors-in-nodejs) |
|34 | [What is the purpose of the path module?](#what-is-the-purpose-of-the-path-module) |
|35 | [What is the difference between app.use() and app.get()?](#what-is-the-difference-between-appuse-and-appget) |
|36 | [What is JWT authentication?](#what-is-jwt-authentication) |
|37 | [What is the purpose of the dotenv package?](#what-is-the-purpose-of-the-dotenv-package) |
|38 | [What is the difference between PUT and PATCH?](#what-is-the-difference-between-put-and-patch) |
|39 | [What is the purpose of body-parser?](#what-is-the-purpose-of-body-parser) |
|40 | [What is the difference between app.listen() and server.listen()?](#what-is-the-difference-between-applisten-and-serverlisten) |
|41 | [What is piping in Node.js?](#what-is-piping-in-nodejs) |
|42 | [What is the purpose of util.promisify()?](#what-is-the-purpose-of-utilpromisify) |
|43 | [What is the difference between Node.js and Ajax?](#what-is-the-difference-between-nodejs-and-ajax) |
|44 | [What is LTS version of Node.js?](#what-is-lts-version-of-nodejs) |
|45 | [What is the purpose of the os module?](#what-is-the-purpose-of-the-os-module) |
|46 | [What is the difference between module.exports and exports?](#what-is-the-difference-between-moduleexports-and-exports) |
|47 | [What is the purpose of the fs module?](#what-is-the-purpose-of-the-fs-module) |
|48 | [What is the difference between setTimeout() and setInterval()?](#what-is-the-difference-between-settimeout-and-setinterval) |
|49 | [What is the purpose of the http module?](#what-is-the-purpose-of-the-http-module) |
|50 | [How do you debug Node.js applications?](#how-do-you-debug-nodejs-applications) |
|51 | [What is backpressure in Node.js?](#what-is-backpressure-in-nodejs) |
|52 | [What are Worker Threads in Node.js?](#what-are-worker-threads-in-nodejs) |
|53 | [What is the difference between cluster and worker threads?](#what-is-the-difference-between-cluster-and-worker-threads) |
|54 | [How do you detect and prevent memory leaks?](#how-do-you-detect-and-prevent-memory-leaks) |
|55 | [What is the Event Loop in detail?](#what-is-the-event-loop-in-detail) |
|56 | [How do you optimize Node.js performance?](#how-do-you-optimize-nodejs-performance) |
|57 | [What are child processes and when to use them?](#what-are-child-processes-and-when-to-use-them) |
|58 | [How do you handle backpressure in streams?](#how-do-you-handle-backpressure-in-streams) |
|59 | [What is garbage collection in Node.js?](#what-is-garbage-collection-in-nodejs) |
|60 | [What are V8 flags and how to use them?](#what-are-v8-flags-and-how-to-use-them) |
|61 | [How do you create a REST API with Express.js?](#how-do-you-create-a-rest-api-with-expressjs) |
|62 | [How do you validate API requests and handle errors in Express.js?](#how-do-you-validate-api-requests-and-handle-errors-in-expressjs) |
|63 | [How do you add pagination and filtering to an API?](#how-do-you-add-pagination-and-filtering-to-an-api) |

---

### 1. What is Node.js?

Node.js is an open-source, cross-platform JavaScript runtime environment that executes JavaScript code outside of a web browser. It is built on Chrome's V8 JavaScript engine and allows developers to use JavaScript for server-side scripting.

**Key Points:**
- Runs on the V8 engine
- Asynchronous and event-driven
- Single-threaded but highly scalable
- Uses non-blocking I/O operations

```javascript
// Simple Node.js server
const http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

**[⬆ Back to Top](#table-of-contents)**

### 2. What are the key features of Node.js?

The key features of Node.js include:

1. **Asynchronous and Event-Driven**: All APIs are asynchronous (non-blocking)
2. **Fast Execution**: Built on Google Chrome's V8 JavaScript engine
3. **Single-Threaded**: Uses a single-threaded model with event looping
4. **Highly Scalable**: Event mechanism helps the server respond in a non-blocking way
5. **No Buffering**: Applications never buffer any data
6. **Cross-Platform**: Works on various platforms (Windows, Linux, Unix, Mac OS X)
7. **NPM**: Largest ecosystem of open-source libraries

```javascript
// Asynchronous example
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});

console.log('This will print first');
```

**[⬆ Back to Top](#table-of-contents)**

### 3. What is the difference between Node.js and JavaScript?

| JavaScript | Node.js |
|-----------|---------|
| Programming language | Runtime environment for JavaScript |
| Runs in browser | Runs on server |
| Used for client-side operations | Used for server-side operations |
| Cannot access file system | Can access file system |
| Limited to browser capabilities | Access to operating system functionalities |
| DOM manipulation possible | No DOM |

```javascript
// JavaScript (Browser)
document.getElementById('demo').innerHTML = 'Hello';

// Node.js (Server)
const fs = require('fs');
fs.writeFileSync('demo.txt', 'Hello');
```

**[⬆ Back to Top](#table-of-contents)**

### 4. What is the V8 engine?

V8 is Google's open-source high-performance JavaScript and WebAssembly engine, written in C++. It is used in Chrome and Node.js. V8 compiles JavaScript directly to native machine code before executing it, instead of using an interpreter.

**Key Features:**
- Just-In-Time (JIT) compilation
- Hidden class transitions for dynamic property access
- Garbage collection for memory management
- Inline caching for faster property access

```javascript
// V8 optimizes this code
function add(a, b) {
  return a + b;
}

// V8 will compile this to machine code
for (let i = 0; i < 1000000; i++) {
  add(i, i + 1);
}
```

**[⬆ Back to Top](#table-of-contents)**

### 5. What is Event Loop in Node.js?

The Event Loop is a mechanism that allows Node.js to perform non-blocking I/O operations despite JavaScript being single-threaded. It continuously checks the call stack and callback queue, executing callbacks when the call stack is empty.

**Event Loop Phases:**
1. Timers (setTimeout, setInterval)
2. Pending callbacks
3. Idle, prepare
4. Poll (retrieve new I/O events)
5. Check (setImmediate)
6. Close callbacks

```javascript
console.log('Start');

setTimeout(() => {
  console.log('Timeout');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise');
});

console.log('End');

// Output:
// Start
// End
// Promise
// Timeout
```

**[⬆ Back to Top](#table-of-contents)**

### 6. What is the purpose of module.exports?

`module.exports` is used to export functions, objects, or values from a module so they can be used in other files using the `require()` function.

```javascript
// math.js
function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

module.exports = {
  add,
  subtract
};

// app.js
const math = require('./math');
console.log(math.add(5, 3)); // 8
console.log(math.subtract(5, 3)); // 2
```

**[⬆ Back to Top](#table-of-contents)**

### 7. What is the difference between require() and import?

| require() | import |
|-----------|--------|
| CommonJS syntax | ES6 module syntax |
| Synchronous | Asynchronous |
| Can be called anywhere | Must be at top of file |
| Dynamic loading possible | Static structure |
| Default in Node.js | Requires ES modules flag or .mjs |

```javascript
// CommonJS (require)
const express = require('express');
const app = express();

// ES6 (import)
import express from 'express';
const app = express();

// Dynamic require
if (condition) {
  const module = require('./module'); // Valid
}

// Import must be at top
import module from './module'; // Must be at top level
```

**[⬆ Back to Top](#table-of-contents)**

### 8. What is npm?

npm (Node Package Manager) is the default package manager for Node.js. It is the world's largest software registry where developers can share and borrow packages.

**Key Features:**
- Install packages
- Manage dependencies
- Run scripts
- Publish packages
- Version management

```bash
# Install a package
npm install express

# Install as dev dependency
npm install --save-dev nodemon

# Install globally
npm install -g typescript

# Run scripts
npm run start

# Update packages
npm update
```

**[⬆ Back to Top](#table-of-contents)**

### 9. What is package.json?

`package.json` is a metadata file that contains information about the Node.js project, including dependencies, scripts, version, author, and more.

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "A Node.js application",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.18.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.15"
  },
  "author": "Your Name",
  "license": "MIT"
}
```

**[⬆ Back to Top](#table-of-contents)**

### 10. What is the difference between dependencies and devDependencies?

| dependencies | devDependencies |
|--------------|-----------------|
| Required for production | Required only for development |
| Installed with `npm install` | Installed with `npm install` |
| Included in production build | Not included in production build |
| Examples: express, mongoose | Examples: nodemon, jest, eslint |

```json
{
  "dependencies": {
    "express": "^4.18.0",
    "mongoose": "^6.0.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.15",
    "jest": "^27.0.0",
    "eslint": "^8.0.0"
  }
}
```

```bash
# Install only production dependencies
npm install --production
```

**[⬆ Back to Top](#table-of-contents)**

### 11. What is callback in Node.js?

A callback is a function passed as an argument to another function, which is executed after the completion of an operation. Callbacks are fundamental to Node.js asynchronous programming.

```javascript
// Callback example
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error reading file:', err);
    return;
  }
  console.log('File content:', data);
});

// Custom callback function
function fetchData(callback) {
  setTimeout(() => {
    const data = { name: 'John', age: 30 };
    callback(null, data);
  }, 1000);
}

fetchData((err, data) => {
  if (err) console.error(err);
  else console.log(data);
});
```

**[⬆ Back to Top](#table-of-contents)**

### 12. What is callback hell?

Callback hell refers to heavily nested callbacks that make code difficult to read and maintain. It occurs when multiple asynchronous operations depend on each other.

```javascript
// Callback hell example
fs.readFile('file1.txt', (err, data1) => {
  if (err) throw err;
  fs.readFile('file2.txt', (err, data2) => {
    if (err) throw err;
    fs.readFile('file3.txt', (err, data3) => {
      if (err) throw err;
      fs.writeFile('output.txt', data1 + data2 + data3, (err) => {
        if (err) throw err;
        console.log('Done!');
      });
    });
  });
});
```

**[⬆ Back to Top](#table-of-contents)**

### 13. How do you prevent callback hell?

You can prevent callback hell using:

1. **Promises**
2. **Async/Await**
3. **Modularization**
4. **Named functions**

```javascript
// Using Promises
const fs = require('fs').promises;

fs.readFile('file1.txt', 'utf8')
  .then(data1 => fs.readFile('file2.txt', 'utf8'))
  .then(data2 => fs.readFile('file3.txt', 'utf8'))
  .then(data3 => console.log('Done'))
  .catch(err => console.error(err));

// Using Async/Await
async function readFiles() {
  try {
    const data1 = await fs.readFile('file1.txt', 'utf8');
    const data2 = await fs.readFile('file2.txt', 'utf8');
    const data3 = await fs.readFile('file3.txt', 'utf8');
    console.log('Done');
  } catch (err) {
    console.error(err);
  }
}

readFiles();
```

**[⬆ Back to Top](#table-of-contents)**

### 14. What are Promises in Node.js?

A Promise is an object representing the eventual completion or failure of an asynchronous operation. It has three states: pending, fulfilled, or rejected.

```javascript
// Creating a Promise
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const success = true;
    if (success) {
      resolve('Operation successful!');
    } else {
      reject('Operation failed!');
    }
  }, 1000);
});

// Using a Promise
myPromise
  .then(result => console.log(result))
  .catch(error => console.error(error))
  .finally(() => console.log('Promise completed'));

// Promise chaining
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

**[⬆ Back to Top](#table-of-contents)**

### 15. What is async/await?

`async/await` is syntactic sugar built on top of Promises, making asynchronous code look and behave more like synchronous code.

```javascript
// async function returns a Promise
async function fetchUser() {
  return { name: 'John', age: 30 };
}

// await pauses execution until Promise resolves
async function getUserData() {
  try {
    const user = await fetchUser();
    console.log(user);
  } catch (error) {
    console.error(error);
  }
}

// Multiple await calls
async function fetchAllData() {
  try {
    const user = await fetchUser();
    const posts = await fetchPosts(user.id);
    const comments = await fetchComments(posts[0].id);
    return { user, posts, comments };
  } catch (error) {
    console.error('Error:', error);
  }
}

// Parallel execution
async function fetchParallel() {
  const [users, posts] = await Promise.all([
    fetchUsers(),
    fetchPosts()
  ]);
  return { users, posts };
}
```

**[⬆ Back to Top](#table-of-contents)**

### 16. What is the difference between synchronous and asynchronous functions?

| Synchronous | Asynchronous |
|-------------|--------------|
| Blocks execution until complete | Non-blocking execution |
| Executes line by line | Executes in background |
| Simple to understand | Requires callbacks/promises |
| Can cause performance issues | Better performance |

```javascript
const fs = require('fs');

// Synchronous - blocks execution
console.log('Start');
const data = fs.readFileSync('file.txt', 'utf8');
console.log(data);
console.log('End');

// Output: Start -> file content -> End

// Asynchronous - non-blocking
console.log('Start');
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
console.log('End');

// Output: Start -> End -> file content
```

**[⬆ Back to Top](#table-of-contents)**

### 17. What are Streams in Node.js?

Streams are objects that allow you to read data from a source or write data to a destination in a continuous manner. They are especially useful for handling large amounts of data.

**Benefits:**
- Memory efficient
- Time efficient
- Composable

```javascript
const fs = require('fs');

// Reading stream
const readStream = fs.createReadStream('input.txt', 'utf8');

readStream.on('data', (chunk) => {
  console.log('Received chunk:', chunk);
});

readStream.on('end', () => {
  console.log('Finished reading');
});

readStream.on('error', (err) => {
  console.error('Error:', err);
});

// Writing stream
const writeStream = fs.createWriteStream('output.txt');
writeStream.write('Hello, ');
writeStream.write('World!');
writeStream.end();
```

**[⬆ Back to Top](#table-of-contents)**

### 18. What are the types of Streams?

There are four types of streams in Node.js:

1. **Readable**: Used for read operations (e.g., fs.createReadStream())
2. **Writable**: Used for write operations (e.g., fs.createWriteStream())
3. **Duplex**: Used for both read and write (e.g., TCP socket)
4. **Transform**: Duplex stream that can modify data (e.g., zlib.createGzip())

```javascript
const fs = require('fs');
const zlib = require('zlib');

// Readable stream
const readable = fs.createReadStream('input.txt');

// Writable stream
const writable = fs.createWriteStream('output.txt');

// Transform stream (compress)
const gzip = zlib.createGzip();

// Pipe streams together
readable
  .pipe(gzip)
  .pipe(fs.createWriteStream('input.txt.gz'));

// Duplex stream example
const { Duplex } = require('stream');

const duplexStream = new Duplex({
  read(size) {
    this.push('data');
    this.push(null);
  },
  write(chunk, encoding, callback) {
    console.log(chunk.toString());
    callback();
  }
});
```

**[⬆ Back to Top](#table-of-contents)**

### 19. What is Buffer in Node.js?

Buffer is a temporary storage for binary data. It is similar to an array of integers but corresponds to a fixed-sized chunk of memory allocated outside the V8 heap.

```javascript
// Creating buffers
const buf1 = Buffer.alloc(10); // Allocate 10 bytes
const buf2 = Buffer.from('Hello'); // From string
const buf3 = Buffer.from([1, 2, 3]); // From array

// Reading and writing
const buf = Buffer.alloc(5);
buf.write('Hello');
console.log(buf.toString()); // Hello

// Buffer operations
const buffer = Buffer.from('Hello World');
console.log(buffer.length); // 11
console.log(buffer.toString('hex')); // 48656c6c6f20576f726c64
console.log(buffer.toString('base64')); // SGVsbG8gV29ybGQ=

// Concatenating buffers
const buf4 = Buffer.from('Hello ');
const buf5 = Buffer.from('World');
const buf6 = Buffer.concat([buf4, buf5]);
console.log(buf6.toString()); // Hello World
```

**[⬆ Back to Top](#table-of-contents)**

### 20. What is middleware in Express.js?

Middleware functions are functions that have access to the request object (req), response object (res), and the next middleware function in the application's request-response cycle.

```javascript
const express = require('express');
const app = express();

// Application-level middleware
app.use((req, res, next) => {
  console.log('Time:', Date.now());
  next();
});

// Router-level middleware
app.use('/user', (req, res, next) => {
  console.log('User route accessed');
  next();
});

// Built-in middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Third-party middleware
const cors = require('cors');
app.use(cors());

// Error-handling middleware
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});

app.listen(3000);
```

**[⬆ Back to Top](#table-of-contents)**

### 21. What is the purpose of next() in middleware?

The `next()` function passes control to the next middleware function. If not called, the request will be left hanging.

```javascript
const express = require('express');
const app = express();

// Middleware 1
app.use((req, res, next) => {
  console.log('Middleware 1');
  next(); // Pass to next middleware
});

// Middleware 2
app.use((req, res, next) => {
  console.log('Middleware 2');
  next(); // Pass to next middleware
});

// Route handler
app.get('/', (req, res) => {
  res.send('Hello World');
});

// Without next() - request hangs
app.use((req, res, next) => {
  console.log('This will hang');
  // next() is not called - request never completes
});

// Pass error to error handler
app.use((req, res, next) => {
  const error = new Error('Something went wrong');
  next(error); // Skip to error-handling middleware
});

app.use((err, req, res, next) => {
  res.status(500).json({ error: err.message });
});
```

**[⬆ Back to Top](#table-of-contents)**

### 22. What is the difference between process.nextTick() and setImmediate()?

| process.nextTick() | setImmediate() |
|-------------------|----------------|
| Executes before I/O events | Executes after I/O events |
| Executes in current phase | Executes in check phase |
| Can cause I/O starvation | Better for I/O operations |
| Higher priority | Lower priority |

```javascript
console.log('Start');

setImmediate(() => {
  console.log('setImmediate');
});

process.nextTick(() => {
  console.log('nextTick');
});

console.log('End');

// Output:
// Start
// End
// nextTick
// setImmediate

// Multiple nextTick calls
process.nextTick(() => console.log('nextTick 1'));
process.nextTick(() => console.log('nextTick 2'));
setImmediate(() => console.log('setImmediate 1'));
setImmediate(() => console.log('setImmediate 2'));

// Output:
// nextTick 1
// nextTick 2
// setImmediate 1
// setImmediate 2
```

**[⬆ Back to Top](#table-of-contents)**

### 23. What is Event Emitter?

EventEmitter is a class in Node.js that allows objects to emit and listen to events. It's a key part of Node.js asynchronous event-driven architecture.

```javascript
const EventEmitter = require('events');

// Create an event emitter
class MyEmitter extends EventEmitter {}
const myEmitter = new MyEmitter();

// Register event listener
myEmitter.on('event', (data) => {
  console.log('Event occurred:', data);
});

// Emit event
myEmitter.emit('event', 'Hello World');

// Multiple listeners
myEmitter.on('greet', () => console.log('Hello!'));
myEmitter.on('greet', () => console.log('Hi!'));
myEmitter.emit('greet');

// Once listener (fires only once)
myEmitter.once('login', (user) => {
  console.log('User logged in:', user);
});

myEmitter.emit('login', 'John'); // Fires
myEmitter.emit('login', 'Jane'); // Does not fire

// Remove listener
const callback = () => console.log('callback');
myEmitter.on('test', callback);
myEmitter.removeListener('test', callback);
```

**[⬆ Back to Top](#table-of-contents)**

### 24. What is the purpose of the cluster module?

The cluster module allows you to create child processes (workers) that share the same server port, enabling you to take advantage of multi-core systems.

```javascript
const cluster = require('cluster');
const http = require('http');
const os = require('os');

if (cluster.isMaster) {
  const numCPUs = os.cpus().length;
  console.log(`Master process ${process.pid} is running`);

  // Fork workers
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  cluster.on('exit', (worker, code, signal) => {
    console.log(`Worker ${worker.process.pid} died`);
    cluster.fork(); // Restart worker
  });
} else {
  // Workers share the TCP connection
  http.createServer((req, res) => {
    res.writeHead(200);
    res.end(`Worker ${process.pid} handled request\n`);
  }).listen(8000);

  console.log(`Worker ${process.pid} started`);
}
```

**[⬆ Back to Top](#table-of-contents)**

### 25. What is the difference between fork() and spawn()?

| fork() | spawn() |
|--------|---------|
| Special case of spawn() | General method to launch processes |
| Creates a new V8 instance | Does not create V8 instance |
| Has IPC channel | No built-in IPC |
| Used for Node.js processes | Used for any process |
| Higher memory usage | Lower memory usage |

```javascript
const { spawn, fork } = require('child_process');

// spawn() - for any command
const ls = spawn('ls', ['-lh', '/usr']);

ls.stdout.on('data', (data) => {
  console.log(`stdout: ${data}`);
});

ls.stderr.on('data', (data) => {
  console.error(`stderr: ${data}`);
});

ls.on('close', (code) => {
  console.log(`child process exited with code ${code}`);
});

// fork() - for Node.js modules
const child = fork('child.js');

child.on('message', (msg) => {
  console.log('Message from child:', msg);
});

child.send({ hello: 'world' });

// child.js
process.on('message', (msg) => {
  console.log('Message from parent:', msg);
  process.send({ received: true });
});
```

**[⬆ Back to Top](#table-of-contents)**

### 26. What is REPL in Node.js?

REPL (Read-Eval-Print-Loop) is an interactive shell that processes Node.js expressions. It's useful for testing JavaScript code, debugging, and experimenting with Node.js APIs.

**REPL Commands:**
- `.help` - Show all commands
- `.break` - Exit multi-line expression
- `.clear` - Reset context
- `.save` - Save session to file
- `.load` - Load file into session
- `.exit` - Exit REPL

```javascript
// Start REPL
// Type 'node' in terminal

// Examples in REPL:
> 2 + 2
4

> const name = 'John'
undefined

> name
'John'

> function add(a, b) { return a + b; }
undefined

> add(5, 3)
8

> const os = require('os')
undefined

> os.platform()
'win32'

// Multi-line input
> function test() {
... console.log('Hello');
... }
undefined

> test()
Hello
```

**[⬆ Back to Top](#table-of-contents)**

### 27. What is the purpose of the crypto module?

The crypto module provides cryptographic functionality including hashing, encryption, decryption, and generating random values.

```javascript
const crypto = require('crypto');

// Hash (MD5, SHA256, etc.)
const hash = crypto.createHash('sha256');
hash.update('password123');
console.log(hash.digest('hex'));

// HMAC (Hash-based Message Authentication Code)
const hmac = crypto.createHmac('sha256', 'secret-key');
hmac.update('data to authenticate');
console.log(hmac.digest('hex'));

// Encryption and Decryption
const algorithm = 'aes-256-cbc';
const key = crypto.randomBytes(32);
const iv = crypto.randomBytes(16);

function encrypt(text) {
  const cipher = crypto.createCipheriv(algorithm, key, iv);
  let encrypted = cipher.update(text, 'utf8', 'hex');
  encrypted += cipher.final('hex');
  return encrypted;
}

function decrypt(encrypted) {
  const decipher = crypto.createDecipheriv(algorithm, key, iv);
  let decrypted = decipher.update(encrypted, 'hex', 'utf8');
  decrypted += decipher.final('utf8');
  return decrypted;
}

// Random bytes
const randomBytes = crypto.randomBytes(16).toString('hex');
console.log(randomBytes);
```

**[⬆ Back to Top](#table-of-contents)**

### 28. What is the difference between readFile and createReadStream?

| readFile | createReadStream |
|----------|------------------|
| Reads entire file into memory | Reads file in chunks |
| Not suitable for large files | Suitable for large files |
| Simple to use | More complex |
| Returns all data at once | Returns data in streams |
| Higher memory usage | Lower memory usage |

```javascript
const fs = require('fs');

// readFile - loads entire file
fs.readFile('large-file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data); // Entire file content
});

// createReadStream - reads in chunks
const readStream = fs.createReadStream('large-file.txt', {
  encoding: 'utf8',
  highWaterMark: 16 * 1024 // 16KB chunks
});

readStream.on('data', (chunk) => {
  console.log('Chunk:', chunk.length);
});

readStream.on('end', () => {
  console.log('Finished reading');
});

// Practical example: Copy large file
const readStream = fs.createReadStream('source.txt');
const writeStream = fs.createWriteStream('destination.txt');
readStream.pipe(writeStream);
```

**[⬆ Back to Top](#table-of-contents)**

### 29. How do you handle errors in Node.js?

Error handling in Node.js can be done using:

1. **Try-Catch** (for synchronous code)
2. **Callbacks** (error-first callbacks)
3. **Promises** (.catch())
4. **Async/Await** (try-catch)
5. **Event Emitters** (error events)
6. **Error Middleware** (Express.js)

```javascript
// Try-Catch
try {
  const data = JSON.parse(invalidJSON);
} catch (error) {
  console.error('Error:', error.message);
}

// Error-first callbacks
fs.readFile('file.txt', (err, data) => {
  if (err) {
    console.error('Error reading file:', err);
    return;
  }
  console.log(data);
});

// Promises
fetchData()
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

// Async/Await
async function getData() {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (error) {
    console.error('Error:', error);
  }
}

// Global error handlers
process.on('uncaughtException', (error) => {
  console.error('Uncaught Exception:', error);
  process.exit(1);
});

process.on('unhandledRejection', (reason, promise) => {
  console.error('Unhandled Rejection at:', promise, 'reason:', reason);
});
```

**[⬆ Back to Top](#table-of-contents)**

### 30. What is global object in Node.js?

The global object in Node.js provides variables and functions that are available in all modules without requiring them.

**Common Global Objects:**
- `__dirname` - Current directory
- `__filename` - Current file
- `console` - Console functions
- `process` - Process information
- `Buffer` - Binary data
- `setTimeout`, `setInterval`, `setImmediate`
- `require()` - Import modules

```javascript
// Global variables
console.log(__dirname); // Current directory path
console.log(__filename); // Current file path
console.log(process.version); // Node.js version

// Custom global variables (not recommended)
global.myVariable = 'Hello';
console.log(myVariable); // Accessible anywhere

// Process object
console.log(process.env.NODE_ENV); // Environment variables
console.log(process.argv); // Command line arguments
console.log(process.pid); // Process ID

// Console
console.log('Log message');
console.error('Error message');
console.warn('Warning message');
console.time('label');
console.timeEnd('label');
```

**[⬆ Back to Top](#table-of-contents)**

### 31. What is the purpose of __dirname and __filename?

- `__dirname`: Returns the absolute path of the directory containing the currently executing file
- `__filename`: Returns the absolute path of the currently executing file

```javascript
// current file: /home/user/project/app.js

console.log(__dirname);  // /home/user/project
console.log(__filename); // /home/user/project/app.js

// Practical usage
const path = require('path');
const fs = require('fs');

// Reading a file in the same directory
const filePath = path.join(__dirname, 'config.json');
const config = JSON.parse(fs.readFileSync(filePath, 'utf8'));

// Serving static files in Express
app.use(express.static(path.join(__dirname, 'public')));

// Creating absolute paths
const uploadDir = path.join(__dirname, 'uploads');
if (!fs.existsSync(uploadDir)) {
  fs.mkdirSync(uploadDir);
}

// Note: __dirname and __filename are not available in ES modules
// Use import.meta.url instead
import { fileURLToPath } from 'url';
import { dirname } from 'path';

const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);
```

**[⬆ Back to Top](#table-of-contents)**

### 32. What is the difference between req.params, req.query and req.body?

| req.params | req.query | req.body |
|------------|-----------|----------|
| Route parameters | URL query string | Request body |
| Part of URL path | After ? in URL | POST/PUT data |
| `/user/:id` | `/search?q=term` | Form data, JSON |

```javascript
const express = require('express');
const app = express();

app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// req.params - Route parameters
// URL: /user/123
app.get('/user/:id', (req, res) => {
  console.log(req.params.id); // "123"
  res.send(`User ID: ${req.params.id}`);
});

// req.query - Query string
// URL: /search?q=nodejs&page=1
app.get('/search', (req, res) => {
  console.log(req.query.q); // "nodejs"
  console.log(req.query.page); // "1"
  res.send(`Search: ${req.query.q}, Page: ${req.query.page}`);
});

// req.body - Request body
// POST /user with body: { "name": "John", "age": 30 }
app.post('/user', (req, res) => {
  console.log(req.body.name); // "John"
  console.log(req.body.age); // 30
  res.send(`Created user: ${req.body.name}`);
});

// Combining all three
// POST /user/123/comments?sort=desc with body
app.post('/user/:id/comments', (req, res) => {
  const userId = req.params.id; // Route parameter
  const sortOrder = req.query.sort; // Query parameter
  const comment = req.body.text; // Body data
  res.send(`User ${userId}, Sort: ${sortOrder}, Comment: ${comment}`);
});
```

**[⬆ Back to Top](#table-of-contents)**

### 33. What is cors in Node.js?

CORS (Cross-Origin Resource Sharing) is a security feature that allows or restricts resources on a web server to be requested from another domain.

```javascript
const express = require('express');
const cors = require('cors');
const app = express();

// Enable CORS for all routes
app.use(cors());

// Configure CORS with options
const corsOptions = {
  origin: 'http://example.com',
  methods: ['GET', 'POST'],
  allowedHeaders: ['Content-Type', 'Authorization'],
  credentials: true,
  optionsSuccessStatus: 200
};

app.use(cors(corsOptions));

// Enable CORS for specific route
app.get('/api/data', cors(), (req, res) => {
  res.json({ data: 'This is CORS-enabled' });
});

// Multiple origins
const whitelist = ['http://example1.com', 'http://example2.com'];
const corsOptionsDelegate = {
  origin: function (origin, callback) {
    if (whitelist.indexOf(origin) !== -1 || !origin) {
      callback(null, true);
    } else {
      callback(new Error('Not allowed by CORS'));
    }
  }
};

app.use(cors(corsOptionsDelegate));

// Manual CORS headers
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', '*');
  res.header('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE');
  res.header('Access-Control-Allow-Headers', 'Content-Type');
  next();
});
```

**[⬆ Back to Top](#table-of-contents)**

### 34. What is the purpose of the path module?

The path module provides utilities for working with file and directory paths in a cross-platform way.

```javascript
const path = require('path');

// Join paths
const fullPath = path.join('/users', 'john', 'documents', 'file.txt');
console.log(fullPath); // /users/john/documents/file.txt

// Resolve absolute path
const absolutePath = path.resolve('folder', 'file.txt');
console.log(absolutePath); // /current/working/directory/folder/file.txt

// Get directory name
console.log(path.dirname('/users/john/file.txt')); // /users/john

// Get file name
console.log(path.basename('/users/john/file.txt')); // file.txt
console.log(path.basename('/users/john/file.txt', '.txt')); // file

// Get file extension
console.log(path.extname('file.txt')); // .txt

// Parse path
const parsed = path.parse('/users/john/file.txt');
console.log(parsed);
// {
//   root: '/',
//   dir: '/users/john',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file'
// }

// Format path
const formatted = path.format({
  dir: '/users/john',
  base: 'file.txt'
});
console.log(formatted); // /users/john/file.txt

// Normalize path
console.log(path.normalize('/users//john/../jane/./file.txt'));
// /users/jane/file.txt

// Check if path is absolute
console.log(path.isAbsolute('/users/john')); // true
console.log(path.isAbsolute('users/john')); // false
```

**[⬆ Back to Top](#table-of-contents)**

### 35. What is the difference between app.use() and app.get()?

| app.use() | app.get() |
|-----------|-----------|
| Middleware function | Route handler |
| Matches all HTTP methods | Only matches GET requests |
| Can match path prefixes | Exact path matching |
| Used for middleware | Used for routes |

```javascript
const express = require('express');
const app = express();

// app.use() - Middleware for all methods
app.use((req, res, next) => {
  console.log('This runs for all requests');
  next();
});

// app.use() - Middleware for specific path prefix
app.use('/api', (req, res, next) => {
  console.log('API route accessed');
  next();
});

// app.use() - Mount middleware
app.use(express.json());

// app.get() - GET request handler
app.get('/users', (req, res) => {
  res.send('GET users');
});

// Other HTTP methods
app.post('/users', (req, res) => {
  res.send('POST user');
});

app.put('/users/:id', (req, res) => {
  res.send('PUT user');
});

app.delete('/users/:id', (req, res) => {
  res.send('DELETE user');
});

// app.use() matches prefixes
app.use('/blog', (req, res) => {
  // Matches /blog, /blog/post, /blog/anything
  res.send('Blog');
});

// app.get() exact match
app.get('/blog', (req, res) => {
  // Only matches /blog
  res.send('Blog home');
});
```

**[⬆ Back to Top](#table-of-contents)**

### 36. What is JWT authentication?

JWT (JSON Web Token) is a compact, URL-safe token format used for authentication and information exchange. It consists of three parts: Header, Payload, and Signature.

```javascript
const jwt = require('jsonwebtoken');
const express = require('express');
const app = express();

const SECRET_KEY = 'your-secret-key';

app.use(express.json());

// Generate JWT token
app.post('/login', (req, res) => {
  const { username, password } = req.body;
  
  // Validate credentials (simplified)
  if (username === 'user' && password === 'pass') {
    const payload = {
      userId: 123,
      username: username,
      role: 'admin'
    };
    
    const token = jwt.sign(payload, SECRET_KEY, { expiresIn: '1h' });
    
    res.json({ token });
  } else {
    res.status(401).json({ error: 'Invalid credentials' });
  }
});

// Middleware to verify JWT
function authenticateToken(req, res, next) {
  const authHeader = req.headers['authorization'];
  const token = authHeader && authHeader.split(' ')[1];
  
  if (!token) {
    return res.status(401).json({ error: 'No token provided' });
  }
  
  jwt.verify(token, SECRET_KEY, (err, decoded) => {
    if (err) {
      return res.status(403).json({ error: 'Invalid token' });
    }
    req.user = decoded;
    next();
  });
}

// Protected route
app.get('/protected', authenticateToken, (req, res) => {
  res.json({
    message: 'Protected data',
    user: req.user
  });
});

// Refresh token
app.post('/refresh', authenticateToken, (req, res) => {
  const newToken = jwt.sign(
    { userId: req.user.userId, username: req.user.username },
    SECRET_KEY,
    { expiresIn: '1h' }
  );
  res.json({ token: newToken });
});
```

**[⬆ Back to Top](#table-of-contents)**

### 37. What is the purpose of the dotenv package?

dotenv is a zero-dependency module that loads environment variables from a `.env` file into `process.env`, helping to keep sensitive data separate from code.

```javascript
// Install: npm install dotenv

// .env file
PORT=3000
DB_HOST=localhost
DB_USER=admin
DB_PASS=secret123
API_KEY=abc123xyz
NODE_ENV=development

// app.js
require('dotenv').config();

const express = require('express');
const app = express();

// Access environment variables
const port = process.env.PORT || 3000;
const dbHost = process.env.DB_HOST;
const apiKey = process.env.API_KEY;

console.log(`Server running on port ${port}`);
console.log(`Database host: ${dbHost}`);

// Database configuration
const dbConfig = {
  host: process.env.DB_HOST,
  user: process.env.DB_USER,
  password: process.env.DB_PASS,
  database: 'myapp'
};

// Different environments
if (process.env.NODE_ENV === 'production') {
  // Production configuration
} else {
  // Development configuration
}

app.listen(port, () => {
  console.log(`Server started on port ${port}`);
});

// Custom path for .env file
require('dotenv').config({ path: './config/.env' });

// .gitignore
// .env
// .env.local
```

**[⬆ Back to Top](#table-of-contents)**

### 38. What is the difference between PUT and PATCH?

| PUT | PATCH |
|-----|-------|
| Replaces entire resource | Partially updates resource |
| Requires all fields | Requires only changed fields |
| Idempotent | Idempotent |
| Creates if not exists | Updates existing resource |

```javascript
const express = require('express');
const app = express();

app.use(express.json());

let user = {
  id: 1,
  name: 'John Doe',
  email: 'john@example.com',
  age: 30,
  address: '123 Main St'
};

// PUT - Replace entire resource
app.put('/user/:id', (req, res) => {
  // All fields required
  user = {
    id: req.params.id,
    name: req.body.name,
    email: req.body.email,
    age: req.body.age,
    address: req.body.address
  };
  
  res.json(user);
});

// Request:
// PUT /user/1
// { "name": "Jane", "email": "jane@example.com", "age": 25, "address": "456 Oak St" }
// Result: Entire user object replaced

// PATCH - Partial update
app.patch('/user/:id', (req, res) => {
  // Only update provided fields
  if (req.body.name) user.name = req.body.name;
  if (req.body.email) user.email = req.body.email;
  if (req.body.age) user.age = req.body.age;
  if (req.body.address) user.address = req.body.address;
  
  res.json(user);
});

// Request:
// PATCH /user/1
// { "email": "newemail@example.com" }
// Result: Only email updated, other fields unchanged

// Better PATCH implementation
app.patch('/user/:id', (req, res) => {
  user = { ...user, ...req.body, id: user.id };
  res.json(user);
});
```

**[⬆ Back to Top](#table-of-contents)**

### 39. What is the purpose of body-parser?

body-parser is middleware that parses incoming request bodies before your handlers. As of Express 4.16+, body-parser is built into Express.

```javascript
// Old way (body-parser package)
const bodyParser = require('body-parser');
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

// New way (built into Express 4.16+)
const express = require('express');
const app = express();

// Parse JSON bodies
app.use(express.json());

// Parse URL-encoded bodies
app.use(express.urlencoded({ extended: true }));

// Parse raw bodies
app.use(express.raw());

// Parse text bodies
app.use(express.text());

// Usage examples
app.post('/json', (req, res) => {
  // Content-Type: application/json
  // Body: { "name": "John", "age": 30 }
  console.log(req.body.name); // John
  res.json({ received: req.body });
});

app.post('/form', (req, res) => {
  // Content-Type: application/x-www-form-urlencoded
  // Body: name=John&age=30
  console.log(req.body.name); // John
  res.send('Form received');
});

// Limit payload size
app.use(express.json({ limit: '10mb' }));

// Custom body parser
app.use((req, res, next) => {
  if (req.headers['content-type'] === 'application/custom') {
    let data = '';
    req.on('data', chunk => data += chunk);
    req.on('end', () => {
      req.body = JSON.parse(data);
      next();
    });
  } else {
    next();
  }
});
```

**[⬆ Back to Top](#table-of-contents)**

### 40. What is the difference between app.listen() and server.listen()?

Both create a server, but `server.listen()` provides more flexibility for advanced configurations like HTTPS or WebSockets.

```javascript
const express = require('express');
const http = require('http');
const https = require('https');
const fs = require('fs');

const app = express();

// app.listen() - Simple HTTP server
app.listen(3000, () => {
  console.log('Server running on port 3000');
});

// Equivalent to:
http.createServer(app).listen(3000);

// server.listen() - HTTP server
const httpServer = http.createServer(app);
httpServer.listen(3000, () => {
  console.log('HTTP server on port 3000');
});

// server.listen() - HTTPS server
const httpsOptions = {
  key: fs.readFileSync('private-key.pem'),
  cert: fs.readFileSync('certificate.pem')
};

const httpsServer = https.createServer(httpsOptions, app);
httpsServer.listen(443, () => {
  console.log('HTTPS server on port 443');
});

// server.listen() - WebSocket server
const { Server } = require('socket.io');
const server = http.createServer(app);
const io = new Server(server);

io.on('connection', (socket) => {
  console.log('User connected');
});

server.listen(3000);

// Multiple servers
const httpServer = http.createServer(app);
const httpsServer = https.createServer(httpsOptions, app);

httpServer.listen(80);
httpsServer.listen(443);
```

**[⬆ Back to Top](#table-of-contents)**

### 41. What is piping in Node.js?

Piping is a mechanism to connect the output of one stream to the input of another stream, enabling efficient data transfer without loading all data into memory.

```javascript
const fs = require('fs');
const zlib = require('zlib');

// Basic piping
const readStream = fs.createReadStream('input.txt');
const writeStream = fs.createWriteStream('output.txt');

readStream.pipe(writeStream);

// Multiple pipes (chaining)
fs.createReadStream('input.txt')
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream('input.txt.gz'));

// HTTP response piping
const http = require('http');
http.createServer((req, res) => {
  const stream = fs.createReadStream('large-file.pdf');
  stream.pipe(res);
}).listen(3000);

// Error handling in pipes
const pipeline = require('stream').pipeline;

pipeline(
  fs.createReadStream('input.txt'),
  zlib.createGzip(),
  fs.createWriteStream('input.txt.gz'),
  (err) => {
    if (err) {
      console.error('Pipeline failed:', err);
    } else {
      console.log('Pipeline succeeded');
    }
  }
);

// Transform stream in pipe
const { Transform } = require('stream');

const upperCase = new Transform({
  transform(chunk, encoding, callback) {
    this.push(chunk.toString().toUpperCase());
    callback();
  }
});

fs.createReadStream('input.txt')
  .pipe(upperCase)
  .pipe(fs.createWriteStream('output.txt'));
```

**[⬆ Back to Top](#table-of-contents)**

### 42. What is the purpose of util.promisify()?

`util.promisify()` converts callback-based functions into Promise-based functions, making them compatible with async/await syntax.

```javascript
const util = require('util');
const fs = require('fs');

// Convert callback to Promise
const readFile = util.promisify(fs.readFile);

// Use with async/await
async function readData() {
  try {
    const data = await readFile('file.txt', 'utf8');
    console.log(data);
  } catch (err) {
    console.error(err);
  }
}

readData();

// Multiple promisify
const writeFile = util.promisify(fs.writeFile);
const mkdir = util.promisify(fs.mkdir);
const readdir = util.promisify(fs.readdir);

async function fileOperations() {
  await mkdir('newDir');
  await writeFile('newDir/file.txt', 'Hello World');
  const files = await readdir('newDir');
  console.log(files);
}

// Custom callback function
function customFunction(arg, callback) {
  setTimeout(() => {
    callback(null, `Result: ${arg}`);
  }, 1000);
}

const promisifiedCustom = util.promisify(customFunction);

promisifiedCustom('test')
  .then(result => console.log(result))
  .catch(err => console.error(err));

// fs.promises (built-in Promise API)
const fsPromises = require('fs').promises;

async function useBuiltInPromises() {
  const data = await fsPromises.readFile('file.txt', 'utf8');
  await fsPromises.writeFile('output.txt', data);
}
```

**[⬆ Back to Top](#table-of-contents)**

### 43. What is the difference between Node.js and Ajax?

| Node.js | Ajax |
|---------|------|
| Server-side technology | Client-side technology |
| JavaScript runtime | Browser technique |
| Runs on server | Runs in browser |
| Can access file system | Cannot access file system |
| Full application framework | HTTP request mechanism |

```javascript
// Node.js - Server-side
const http = require('http');
const fs = require('fs');

http.createServer((req, res) => {
  // Can access file system
  const data = fs.readFileSync('data.json');
  res.end(data);
}).listen(3000);

// Ajax - Client-side (Browser)
// Using Fetch API
fetch('http://localhost:3000/api/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));

// Using XMLHttpRequest
const xhr = new XMLHttpRequest();
xhr.open('GET', 'http://localhost:3000/api/data');
xhr.onload = function() {
  if (xhr.status === 200) {
    console.log(JSON.parse(xhr.responseText));
  }
};
xhr.send();

// Node.js can make HTTP requests too
const https = require('https');

https.get('https://api.example.com/data', (res) => {
  let data = '';
  res.on('data', chunk => data += chunk);
  res.on('end', () => console.log(JSON.parse(data)));
});

// Or using axios (works in both)
const axios = require('axios');
axios.get('https://api.example.com/data')
  .then(response => console.log(response.data));
```

**[⬆ Back to Top](#table-of-contents)**

### 44. What is LTS version of Node.js?

LTS (Long Term Support) is a version of Node.js that receives stable updates and security fixes for an extended period (typically 30 months).

**LTS Release Schedule:**
- **Active LTS**: Actively maintained with all updates
- **Maintenance LTS**: Critical bug fixes and security updates only
- **Current**: Latest features but shorter support

```javascript
// Check Node.js version
console.log(process.version); // v18.16.0

// Check if LTS
node --version

// LTS versions (examples):
// v18.x - Active LTS (Hydrogen)
// v16.x - Maintenance LTS (Gallium)
// v14.x - End of Life

// Use nvm to manage versions
// Install LTS version
nvm install --lts

// Install specific version
nvm install 18.16.0

// Use specific version
nvm use 18

// List installed versions
nvm list

// package.json - Specify Node version
{
  "engines": {
    "node": ">=18.0.0"
  }
}

// .nvmrc file
18.16.0

// Benefits of LTS:
// 1. Stability
// 2. Long-term support
// 3. Security updates
// 4. Recommended for production
```

**[⬆ Back to Top](#table-of-contents)**

### 45. What is the purpose of the os module?

The os module provides operating system-related utility methods and properties.

```javascript
const os = require('os');

// Platform information
console.log(os.platform()); // 'win32', 'linux', 'darwin'
console.log(os.type()); // 'Windows_NT', 'Linux', 'Darwin'
console.log(os.arch()); // 'x64', 'arm', 'ia32'
console.log(os.release()); // OS release version

// CPU information
console.log(os.cpus()); // Array of CPU cores
console.log(os.cpus().length); // Number of cores

// Memory information
console.log(os.totalmem()); // Total memory in bytes
console.log(os.freemem()); // Free memory in bytes

// Convert to GB
const totalMemGB = (os.totalmem() / 1024 / 1024 / 1024).toFixed(2);
console.log(`Total Memory: ${totalMemGB} GB`);

// User information
console.log(os.userInfo());
// {
//   username: 'user',
//   homedir: '/home/user',
//   shell: '/bin/bash'
// }

// Network interfaces
console.log(os.networkInterfaces());

// System uptime
console.log(os.uptime()); // Seconds since system boot

// Temporary directory
console.log(os.tmpdir()); // /tmp or C:\Users\...\AppData\Local\Temp

// Hostname
console.log(os.hostname());

// End of line marker
console.log(os.EOL); // '\n' on POSIX, '\r\n' on Windows

// Constants
console.log(os.constants.signals); // Signal constants
console.log(os.constants.errno); // Error constants
```

**[⬆ Back to Top](#table-of-contents)**

### 46. What is the difference between module.exports and exports?

`exports` is a shorthand reference to `module.exports`. However, assigning directly to `exports` breaks the reference.

```javascript
// They point to the same object initially
console.log(exports === module.exports); // true

// ✅ CORRECT - Adding properties
exports.add = function(a, b) {
  return a + b;
};

module.exports.subtract = function(a, b) {
  return a - b;
};

// Both work the same way above

// ❌ WRONG - Assigning to exports
exports = function() {
  console.log('This will NOT work');
};
// exports is now a different object, not exported

// ✅ CORRECT - Assigning to module.exports
module.exports = function() {
  console.log('This WILL work');
};

// Practical examples

// math.js - Using exports
exports.add = (a, b) => a + b;
exports.multiply = (a, b) => a * b;

// app.js
const math = require('./math');
console.log(math.add(2, 3)); // 5

// calculator.js - Using module.exports
module.exports = class Calculator {
  add(a, b) { return a + b; }
  subtract(a, b) { return a - b; }
};

// app.js
const Calculator = require('./calculator');
const calc = new Calculator();
console.log(calc.add(5, 3)); // 8

// Best practice: Use module.exports for clarity
module.exports = {
  add: (a, b) => a + b,
  subtract: (a, b) => a - b
};
```

**[⬆ Back to Top](#table-of-contents)**

### 47. What is the purpose of the fs module?

The fs (File System) module provides an API for interacting with the file system, including reading, writing, and manipulating files and directories.

```javascript
const fs = require('fs');
const fsPromises = require('fs').promises;

// Read file (synchronous)
const data = fs.readFileSync('file.txt', 'utf8');
console.log(data);

// Read file (asynchronous - callback)
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});

// Read file (Promise)
fsPromises.readFile('file.txt', 'utf8')
  .then(data => console.log(data))
  .catch(err => console.error(err));

// Write file
fs.writeFileSync('output.txt', 'Hello World');
fs.writeFile('output.txt', 'Hello World', (err) => {
  if (err) throw err;
});

// Append to file
fs.appendFileSync('log.txt', 'New log entry\n');

// Delete file
fs.unlinkSync('file.txt');
fs.unlink('file.txt', (err) => {
  if (err) throw err;
});

// Check if file exists
if (fs.existsSync('file.txt')) {
  console.log('File exists');
}

// Get file stats
const stats = fs.statSync('file.txt');
console.log(stats.isFile());
console.log(stats.isDirectory());
console.log(stats.size);

// Directory operations
fs.mkdirSync('newDir');
fs.rmdirSync('oldDir');
const files = fs.readdirSync('directory');

// Watch file changes
fs.watch('file.txt', (eventType, filename) => {
  console.log(`${filename} changed: ${eventType}`);
});

// Copy file
fs.copyFileSync('source.txt', 'destination.txt');

// Rename/Move file
fs.renameSync('old.txt', 'new.txt');
```

**[⬆ Back to Top](#table-of-contents)**

### 48. What is the difference between setTimeout() and setInterval()?

| setTimeout() | setInterval() |
|--------------|---------------|
| Executes once after delay | Executes repeatedly |
| Single execution | Multiple executions |
| Needs re-calling for repeat | Automatically repeats |

```javascript
// setTimeout - Execute once after delay
setTimeout(() => {
  console.log('Executed after 2 seconds');
}, 2000);

// setTimeout with parameters
setTimeout((name, age) => {
  console.log(`Name: ${name}, Age: ${age}`);
}, 1000, 'John', 30);

// Clear timeout
const timeoutId = setTimeout(() => {
  console.log('This will not execute');
}, 5000);

clearTimeout(timeoutId);

// setInterval - Execute repeatedly
const intervalId = setInterval(() => {
  console.log('Executed every 2 seconds');
}, 2000);

// Clear interval after 10 seconds
setTimeout(() => {
  clearInterval(intervalId);
  console.log('Interval cleared');
}, 10000);

// Recursive setTimeout (alternative to setInterval)
function repeatTask() {
  console.log('Task executed');
  setTimeout(repeatTask, 2000);
}
repeatTask();

// Practical example: Polling
let attempts = 0;
const maxAttempts = 5;

const pollInterval = setInterval(async () => {
  attempts++;
  console.log(`Polling attempt ${attempts}`);
  
  const result = await checkStatus();
  
  if (result.isReady || attempts >= maxAttempts) {
    clearInterval(pollInterval);
    console.log('Polling complete');
  }
}, 3000);

// setImmediate (Node.js specific)
setImmediate(() => {
  console.log('Executed immediately after I/O events');
});
```

**[⬆ Back to Top](#table-of-contents)**

### 49. What is the purpose of the http module?

The http module allows Node.js to create HTTP servers and make HTTP requests.

```javascript
const http = require('http');

// Create HTTP server
const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(3000, () => {
  console.log('Server running on port 3000');
});

// Handle different routes
const server2 = http.createServer((req, res) => {
  const { method, url } = req;
  
  if (url === '/' && method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.end('<h1>Home Page</h1>');
  } else if (url === '/api/users' && method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ users: ['John', 'Jane'] }));
  } else if (url === '/api/users' && method === 'POST') {
    let body = '';
    req.on('data', chunk => body += chunk);
    req.on('end', () => {
      const data = JSON.parse(body);
      res.writeHead(201, { 'Content-Type': 'application/json' });
      res.end(JSON.stringify({ message: 'User created', data }));
    });
  } else {
    res.writeHead(404, { 'Content-Type': 'text/plain' });
    res.end('Not Found');
  }
});

// Make HTTP GET request
http.get('http://api.example.com/data', (res) => {
  let data = '';
  
  res.on('data', (chunk) => {
    data += chunk;
  });
  
  res.on('end', () => {
    console.log(JSON.parse(data));
  });
}).on('error', (err) => {
  console.error('Error:', err);
});

// Make HTTP POST request
const options = {
  hostname: 'api.example.com',
  port: 80,
  path: '/users',
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  }
};

const req = http.request(options, (res) => {
  console.log(`Status: ${res.statusCode}`);
  res.on('data', (chunk) => {
    console.log(chunk.toString());
  });
});

req.on('error', (err) => {
  console.error('Error:', err);
});

req.write(JSON.stringify({ name: 'John', age: 30 }));
req.end();
```

**[⬆ Back to Top](#table-of-contents)**

### 50. How do you debug Node.js applications?

There are multiple ways to debug Node.js applications:

1. **console.log()**
2. **Node.js debugger**
3. **Chrome DevTools**
4. **VS Code debugger**
5. **Debug module**

```javascript
// 1. Console logging
console.log('Debug message');
console.error('Error message');
console.warn('Warning message');
console.dir(object, { depth: null }); // Deep object inspection
console.table([{ name: 'John', age: 30 }]);
console.time('label');
// ... code to measure
console.timeEnd('label');

// 2. Node.js built-in debugger
// Run: node inspect app.js
debugger; // Breakpoint

function add(a, b) {
  debugger; // Execution pauses here
  return a + b;
}

// 3. Chrome DevTools
// Run: node --inspect app.js
// Open: chrome://inspect

// 4. VS Code debugger
// .vscode/launch.json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Launch Program",
      "program": "${workspaceFolder}/app.js",
      "skipFiles": ["<node_internals>/**"]
    }
  ]
}

// 5. Debug module
const debug = require('debug')('app');

debug('Application started');
debug('User %s logged in', 'John');

// Run with: DEBUG=app node app.js

// Error stack traces
try {
  throw new Error('Something went wrong');
} catch (err) {
  console.error(err.stack);
}

// Logging to file
const fs = require('fs');
const logStream = fs.createWriteStream('app.log', { flags: 'a' });

function log(message) {
  const timestamp = new Date().toISOString();
  logStream.write(`${timestamp}: ${message}\n`);
}

// Performance monitoring
console.time('operation');
// ... expensive operation
console.timeEnd('operation');

// Memory usage
console.log(process.memoryUsage());
```

**[⬆ Back to Top](#table-of-contents)**

---

## Advanced Questions

### 51. What is backpressure in Node.js?

Backpressure occurs when the data producer writes data faster than the consumer can read it. This can lead to memory issues if not handled properly. Node.js streams have built-in backpressure handling.

**Why Backpressure Happens:**
- Fast data source (reading from disk)
- Slow data destination (writing to network)
- Buffer overflow
- Memory exhaustion

```javascript
const fs = require('fs');

// ❌ BAD - No backpressure handling
const readStream = fs.createReadStream('large-file.txt');
const writeStream = fs.createWriteStream('output.txt');

readStream.on('data', (chunk) => {
  writeStream.write(chunk); // May cause backpressure
});

// ✅ GOOD - Using pipe() handles backpressure automatically
readStream.pipe(writeStream);

// ✅ GOOD - Manual backpressure handling
readStream.on('data', (chunk) => {
  const canContinue = writeStream.write(chunk);
  
  if (!canContinue) {
    // Pause reading until drain event
    readStream.pause();
  }
});

writeStream.on('drain', () => {
  // Resume reading when buffer is drained
  readStream.resume();
});

// Using pipeline for better error handling
const { pipeline } = require('stream');

pipeline(
  fs.createReadStream('input.txt'),
  fs.createWriteStream('output.txt'),
  (err) => {
    if (err) {
      console.error('Pipeline failed:', err);
    } else {
      console.log('Pipeline succeeded');
    }
  }
);

// Transform stream with backpressure
const { Transform } = require('stream');

const slowTransform = new Transform({
  transform(chunk, encoding, callback) {
    // Simulate slow processing
    setTimeout(() => {
      this.push(chunk.toString().toUpperCase());
      callback();
    }, 100);
  }
});

fs.createReadStream('input.txt')
  .pipe(slowTransform)
  .pipe(fs.createWriteStream('output.txt'));
```

**[⬆ Back to Top](#table-of-contents)**

### 52. What are Worker Threads in Node.js?

Worker Threads allow you to run JavaScript operations in parallel threads, useful for CPU-intensive tasks without blocking the main event loop.

**When to Use:**
- CPU-intensive operations (image processing, encryption)
- Heavy computations
- Parallel processing
- Don't use for I/O operations (already non-blocking)

```javascript
// main.js
const { Worker } = require('worker_threads');

// Create a worker
const worker = new Worker('./worker.js', {
  workerData: { num: 5 }
});

// Listen for messages from worker
worker.on('message', (result) => {
  console.log('Result from worker:', result);
});

worker.on('error', (error) => {
  console.error('Worker error:', error);
});

worker.on('exit', (code) => {
  console.log(`Worker exited with code ${code}`);
});

// Send message to worker
worker.postMessage({ command: 'start' });

// worker.js
const { parentPort, workerData } = require('worker_threads');

// CPU-intensive function
function fibonacci(n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

// Listen for messages from main thread
parentPort.on('message', (msg) => {
  if (msg.command === 'start') {
    const result = fibonacci(workerData.num);
    parentPort.postMessage(result);
  }
});

// Worker pool example
class WorkerPool {
  constructor(workerScript, poolSize) {
    this.workerScript = workerScript;
    this.poolSize = poolSize;
    this.workers = [];
    this.freeWorkers = [];
    this.queue = [];
    
    for (let i = 0; i < poolSize; i++) {
      this.addWorker();
    }
  }
  
  addWorker() {
    const worker = new Worker(this.workerScript);
    this.workers.push(worker);
    this.freeWorkers.push(worker);
    
    worker.on('message', (result) => {
      // Worker is done, make it available
      this.freeWorkers.push(worker);
      this.processQueue();
    });
  }
  
  async runTask(data) {
    return new Promise((resolve, reject) => {
      const task = { data, resolve, reject };
      
      if (this.freeWorkers.length > 0) {
        this.executeTask(task);
      } else {
        this.queue.push(task);
      }
    });
  }
  
  executeTask(task) {
    const worker = this.freeWorkers.pop();
    worker.postMessage(task.data);
    
    worker.once('message', (result) => {
      task.resolve(result);
    });
    
    worker.once('error', (error) => {
      task.reject(error);
    });
  }
  
  processQueue() {
    if (this.queue.length > 0 && this.freeWorkers.length > 0) {
      const task = this.queue.shift();
      this.executeTask(task);
    }
  }
}

// Usage
const pool = new WorkerPool('./worker.js', 4);

async function main() {
  const results = await Promise.all([
    pool.runTask({ num: 40 }),
    pool.runTask({ num: 41 }),
    pool.runTask({ num: 42 })
  ]);
  console.log('Results:', results);
}
```

**[⬆ Back to Top](#table-of-contents)**

### 53. What is the difference between cluster and worker threads?

Both allow parallel processing, but they serve different purposes and work differently.

| Cluster | Worker Threads |
|---------|---------------|
| Multiple processes | Multiple threads in one process |
| Share server ports | Share memory (SharedArrayBuffer) |
| Each has its own memory | Share same memory space |
| Better for I/O scaling | Better for CPU-intensive tasks |
| Higher overhead | Lower overhead |
| Communication via IPC | Communication via message passing |
| Each has own event loop | Share event loop resources |

```javascript
// CLUSTER - For I/O scaling
const cluster = require('cluster');
const http = require('http');
const os = require('os');

if (cluster.isMaster) {
  const numCPUs = os.cpus().length;
  
  // Fork workers (separate processes)
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }
  
  cluster.on('exit', (worker) => {
    console.log(`Worker ${worker.process.pid} died`);
    cluster.fork(); // Restart
  });
} else {
  // Each worker is a separate process
  http.createServer((req, res) => {
    res.end(`Worker ${process.pid}`);
  }).listen(8000);
  
  console.log(`Worker ${process.pid} started`);
}

// WORKER THREADS - For CPU-intensive tasks
const { Worker, isMainThread, parentPort } = require('worker_threads');

if (isMainThread) {
  // Main thread
  const worker = new Worker(__filename);
  
  worker.on('message', (msg) => {
    console.log('From worker:', msg);
  });
  
  worker.postMessage('Hello from main thread');
} else {
  // Worker thread (same process, different thread)
  parentPort.on('message', (msg) => {
    console.log('From main:', msg);
    
    // CPU-intensive work
    const result = heavyComputation();
    parentPort.postMessage(result);
  });
}

// Combining both for optimal performance
if (cluster.isMaster) {
  // Master process forks workers
  for (let i = 0; i < os.cpus().length; i++) {
    cluster.fork();
  }
} else {
  // Each cluster worker can use worker threads
  const express = require('express');
  const app = express();
  
  app.get('/compute', async (req, res) => {
    // Offload CPU work to worker thread
    const worker = new Worker('./compute-worker.js', {
      workerData: req.query
    });
    
    worker.on('message', (result) => {
      res.json({ result });
    });
  });
  
  app.listen(3000);
}

// When to use what:
// 1. Cluster: Scale HTTP server across CPU cores
// 2. Worker Threads: CPU-intensive operations (crypto, image processing)
// 3. Child Process: Running external programs
// 4. Async I/O: Most I/O operations (already non-blocking)
```

**[⬆ Back to Top](#table-of-contents)**

### 54. How do you detect and prevent memory leaks?

Memory leaks occur when memory that is no longer needed is not released. Node.js provides several tools to detect and prevent them.

**Common Causes:**
- Global variables
- Forgotten timers/callbacks
- Event listeners not removed
- Closures holding references
- Large caches without limits

```javascript
// ❌ MEMORY LEAK EXAMPLES

// 1. Global variables
global.cache = {};
function addToCache(key, value) {
  global.cache[key] = value; // Never cleared
}

// 2. Forgotten timers
function startTimer() {
  setInterval(() => {
    console.log('Running...');
  }, 1000);
  // Timer never cleared
}

// 3. Event listeners
const EventEmitter = require('events');
const emitter = new EventEmitter();

function addListener() {
  emitter.on('event', () => {
    console.log('Event fired');
  });
  // Listener never removed
}

// 4. Closures
function createLeak() {
  const largeData = new Array(1000000).fill('data');
  return function() {
    console.log(largeData[0]); // Holds reference to largeData
  };
}

// ✅ PREVENTING MEMORY LEAKS

// 1. Clear timers
function startTimerSafe() {
  const timer = setInterval(() => {
    console.log('Running...');
  }, 1000);
  
  // Clear when done
  setTimeout(() => {
    clearInterval(timer);
  }, 10000);
  
  return timer;
}

// 2. Remove event listeners
function addListenerSafe() {
  const handler = () => console.log('Event fired');
  emitter.on('event', handler);
  
  // Remove when done
  return () => emitter.removeListener('event', handler);
}

// 3. Use WeakMap/WeakSet
const weakCache = new WeakMap();
function addToWeakCache(obj, value) {
  weakCache.set(obj, value);
  // Automatically garbage collected when obj is no longer referenced
}

// 4. Limit cache size
class LRUCache {
  constructor(maxSize) {
    this.maxSize = maxSize;
    this.cache = new Map();
  }
  
  set(key, value) {
    if (this.cache.size >= this.maxSize) {
      const firstKey = this.cache.keys().next().value;
      this.cache.delete(firstKey);
    }
    this.cache.set(key, value);
  }
  
  get(key) {
    return this.cache.get(key);
  }
}

// DETECTING MEMORY LEAKS

// 1. Using process.memoryUsage()
function monitorMemory() {
  const usage = process.memoryUsage();
  console.log({
    rss: `${Math.round(usage.rss / 1024 / 1024)} MB`,
    heapTotal: `${Math.round(usage.heapTotal / 1024 / 1024)} MB`,
    heapUsed: `${Math.round(usage.heapUsed / 1024 / 1024)} MB`,
    external: `${Math.round(usage.external / 1024 / 1024)} MB`
  });
}

setInterval(monitorMemory, 5000);

// 2. Using heap snapshots
const v8 = require('v8');
const fs = require('fs');

function takeHeapSnapshot() {
  const filename = `heap-${Date.now()}.heapsnapshot`;
  const snapshot = v8.writeHeapSnapshot(filename);
  console.log('Snapshot written to', snapshot);
}

// 3. Using Node.js --inspect flag
// Run: node --inspect app.js
// Open chrome://inspect in Chrome
// Take heap snapshots and compare

// 4. Using clinic.js
// npm install -g clinic
// clinic doctor -- node app.js
// clinic heapprofiler -- node app.js

// 5. Monitor with process events
process.on('warning', (warning) => {
  console.warn(warning.name);
  console.warn(warning.message);
  console.warn(warning.stack);
});

// 6. Set memory limits
// node --max-old-space-size=4096 app.js

// Best practices
// - Use 'use strict'
// - Avoid global variables
// - Clean up timers and listeners
// - Use WeakMap/WeakSet for caches
// - Implement cache size limits
// - Monitor memory in production
// - Use proper error handling
```

**[⬆ Back to Top](#table-of-contents)**

### 55. What is the Event Loop in detail?

The Event Loop is the heart of Node.js asynchronous architecture. It has six phases that execute in a specific order.

**Event Loop Phases:**
1. **Timers**: Executes callbacks scheduled by setTimeout/setInterval
2. **Pending callbacks**: Executes I/O callbacks deferred to next iteration
3. **Idle, prepare**: Internal use only
4. **Poll**: Retrieve new I/O events, execute I/O callbacks
5. **Check**: Execute setImmediate callbacks
6. **Close callbacks**: Execute close event callbacks (socket.on('close'))

```javascript
// Phase 1: Timers
setTimeout(() => {
  console.log('setTimeout');
}, 0);

// Phase 4: Poll phase
fs.readFile('file.txt', () => {
  console.log('fs.readFile');
});

// Phase 5: Check
setImmediate(() => {
  console.log('setImmediate');
});

// Microtasks (executed between phases)
Promise.resolve().then(() => {
  console.log('Promise');
});

process.nextTick(() => {
  console.log('nextTick');
});

// Execution order:
// 1. nextTick (highest priority)
// 2. Promise (microtask)
// 3. setTimeout (timer phase)
// 4. setImmediate (check phase)
// 5. fs.readFile (poll phase)

// Detailed example
console.log('1: Sync start');

setTimeout(() => {
  console.log('2: setTimeout 0');
  
  Promise.resolve().then(() => {
    console.log('3: Promise in setTimeout');
  });
  
  process.nextTick(() => {
    console.log('4: nextTick in setTimeout');
  });
}, 0);

setImmediate(() => {
  console.log('5: setImmediate');
  
  process.nextTick(() => {
    console.log('6: nextTick in setImmediate');
  });
});

Promise.resolve().then(() => {
  console.log('7: Promise');
  
  process.nextTick(() => {
    console.log('8: nextTick in Promise');
  });
});

process.nextTick(() => {
  console.log('9: nextTick');
  
  Promise.resolve().then(() => {
    console.log('10: Promise in nextTick');
  });
});

console.log('11: Sync end');

// Output order:
// 1: Sync start
// 11: Sync end
// 9: nextTick (nextTick queue drains first)
// 7: Promise (microtask queue)
// 8: nextTick in Promise
// 10: Promise in nextTick
// 2: setTimeout 0 (timer phase)
// 4: nextTick in setTimeout
// 3: Promise in setTimeout
// 5: setImmediate (check phase)
// 6: nextTick in setImmediate

// Priority order:
// 1. process.nextTick() - highest priority
// 2. Promises (microtasks)
// 3. setTimeout/setInterval
// 4. setImmediate
// 5. I/O callbacks

// Event loop blocking example
function blockEventLoop() {
  const start = Date.now();
  while (Date.now() - start < 5000) {
    // Blocks for 5 seconds
  }
}

// This blocks all async operations
setTimeout(() => console.log('This will be delayed'), 0);
blockEventLoop();

// Non-blocking alternative using setImmediate
function heavyTask() {
  // Do some work
  let result = 0;
  for (let i = 0; i < 1000000; i++) {
    result += i;
  }
  
  // If more work needed, schedule for next iteration
  if (moreWork) {
    setImmediate(heavyTask);
  }
}
```

**[⬆ Back to Top](#table-of-contents)**

### 56. How do you optimize Node.js performance?

Performance optimization in Node.js involves multiple strategies at different levels.

```javascript
// 1. USE CLUSTERING
const cluster = require('cluster');
const os = require('os');

if (cluster.isMaster) {
  for (let i = 0; i < os.cpus().length; i++) {
    cluster.fork();
  }
} else {
  require('./app');
}

// 2. IMPLEMENT CACHING
const NodeCache = require('node-cache');
const cache = new NodeCache({ stdTTL: 600 });

app.get('/api/data/:id', async (req, res) => {
  const cacheKey = `data_${req.params.id}`;
  
  // Check cache first
  const cached = cache.get(cacheKey);
  if (cached) {
    return res.json(cached);
  }
  
  // Fetch from database
  const data = await db.getData(req.params.id);
  
  // Store in cache
  cache.set(cacheKey, data);
  res.json(data);
});

// 3. USE COMPRESSION
const compression = require('compression');
app.use(compression());

// 4. OPTIMIZE DATABASE QUERIES
// ❌ BAD - N+1 query problem
async function getUsersWithPosts() {
  const users = await User.find();
  for (let user of users) {
    user.posts = await Post.find({ userId: user.id });
  }
  return users;
}

// ✅ GOOD - Single query with join
async function getUsersWithPostsOptimized() {
  return User.find().populate('posts');
}

// 5. USE STREAMS FOR LARGE DATA
// ❌ BAD - Loads entire file into memory
app.get('/download', (req, res) => {
  const data = fs.readFileSync('large-file.zip');
  res.send(data);
});

// ✅ GOOD - Streams data
app.get('/download', (req, res) => {
  const stream = fs.createReadStream('large-file.zip');
  stream.pipe(res);
});

// 6. IMPLEMENT CONNECTION POOLING
const { Pool } = require('pg');
const pool = new Pool({
  max: 20,
  idleTimeoutMillis: 30000,
  connectionTimeoutMillis: 2000,
});

// 7. USE ASYNC/AWAIT PROPERLY
// ❌ BAD - Sequential execution
async function fetchDataSlow() {
  const user = await getUser();
  const posts = await getPosts();
  const comments = await getComments();
  return { user, posts, comments };
}

// ✅ GOOD - Parallel execution
async function fetchDataFast() {
  const [user, posts, comments] = await Promise.all([
    getUser(),
    getPosts(),
    getComments()
  ]);
  return { user, posts, comments };
}

// 8. OPTIMIZE REGULAR EXPRESSIONS
// ❌ BAD - Catastrophic backtracking
const badRegex = /^(a+)+$/;

// ✅ GOOD - Optimized
const goodRegex = /^a+$/;

// 9. USE WORKER THREADS FOR CPU-INTENSIVE TASKS
const { Worker } = require('worker_threads');

app.post('/process-image', (req, res) => {
  const worker = new Worker('./image-processor.js', {
    workerData: req.body.image
  });
  
  worker.on('message', (result) => {
    res.json(result);
  });
});

// 10. IMPLEMENT RATE LIMITING
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100 // limit each IP to 100 requests per windowMs
});

app.use('/api/', limiter);

// 11. OPTIMIZE JSON PARSING
// Use fast-json-stringify for serialization
const fastJson = require('fast-json-stringify');
const stringify = fastJson({
  type: 'object',
  properties: {
    name: { type: 'string' },
    age: { type: 'number' }
  }
});

app.get('/user', (req, res) => {
  const user = { name: 'John', age: 30 };
  res.send(stringify(user));
});

// 12. USE PROFILING TOOLS
// Run with profiling: node --prof app.js
// Process profiling data: node --prof-process isolate-*.log

// 13. MONITOR PERFORMANCE
const monitoring = {
  requestCount: 0,
  responseTime: [],
  
  middleware(req, res, next) {
    const start = Date.now();
    this.requestCount++;
    
    res.on('finish', () => {
      const duration = Date.now() - start;
      this.responseTime.push(duration);
      
      if (this.responseTime.length > 1000) {
        this.responseTime.shift();
      }
    });
    
    next();
  },
  
  getStats() {
    const avg = this.responseTime.reduce((a, b) => a + b, 0) / this.responseTime.length;
    return {
      totalRequests: this.requestCount,
      avgResponseTime: avg.toFixed(2),
      memoryUsage: process.memoryUsage()
    };
  }
};

app.use(monitoring.middleware.bind(monitoring));

// 14. ENABLE HTTP/2
const http2 = require('http2');
const server = http2.createSecureServer({
  key: fs.readFileSync('server-key.pem'),
  cert: fs.readFileSync('server-cert.pem')
}, app);

// 15. LAZY LOAD MODULES
// ❌ BAD - Load all modules upfront
const heavy1 = require('./heavy-module-1');
const heavy2 = require('./heavy-module-2');

// ✅ GOOD - Load only when needed
app.get('/feature1', (req, res) => {
  const heavy1 = require('./heavy-module-1');
  heavy1.process();
});
```

**[⬆ Back to Top](#table-of-contents)**

### 57. What are child processes and when to use them?

Child processes allow you to execute external commands, run Node.js scripts in separate processes, or spawn system commands.

**Four Types:**
1. `exec()` - Spawns shell and buffers output
2. `execFile()` - Like exec but without shell
3. `spawn()` - Streams output, more efficient
4. `fork()` - Special spawn for Node.js modules

```javascript
const { exec, execFile, spawn, fork } = require('child_process');

// 1. exec() - Simple command execution
exec('ls -la', (error, stdout, stderr) => {
  if (error) {
    console.error(`Error: ${error}`);
    return;
  }
  console.log(`stdout: ${stdout}`);
  console.error(`stderr: ${stderr}`);
});

// With options
exec('pwd', {
  cwd: '/home/user',
  env: { ...process.env, CUSTOM_VAR: 'value' }
}, (error, stdout) => {
  console.log(stdout);
});

// 2. execFile() - Execute binary/file without shell
execFile('node', ['--version'], (error, stdout) => {
  if (error) throw error;
  console.log(stdout);
});

// 3. spawn() - For large output or streaming
const ls = spawn('ls', ['-lh', '/usr']);

ls.stdout.on('data', (data) => {
  console.log(`stdout: ${data}`);
});

ls.stderr.on('data', (data) => {
  console.error(`stderr: ${data}`);
});

ls.on('close', (code) => {
  console.log(`child process exited with code ${code}`);
});

// spawn() with piping
const grep = spawn('grep', ['ssh']);
const ps = spawn('ps', ['ax']);

ps.stdout.pipe(grep.stdin);

grep.stdout.on('data', (data) => {
  console.log(data.toString());
});

// 4. fork() - Run Node.js modules
const child = fork('child.js');

// Send message to child
child.send({ hello: 'world' });

// Receive message from child
child.on('message', (msg) => {
  console.log('Message from child:', msg);
});

child.on('exit', (code) => {
  console.log(`Child exited with code ${code}`);
});

// child.js
process.on('message', (msg) => {
  console.log('Message from parent:', msg);
  
  // Do some work
  const result = heavyComputation();
  
  // Send result back
  process.send({ result });
});

// REAL-WORLD EXAMPLES

// 1. Image processing
function processImage(imagePath) {
  return new Promise((resolve, reject) => {
    const child = spawn('convert', [
      imagePath,
      '-resize', '800x600',
      '-quality', '85',
      'output.jpg'
    ]);
    
    child.on('exit', (code) => {
      if (code === 0) resolve('output.jpg');
      else reject(new Error('Processing failed'));
    });
  });
}

// 2. Running Python scripts
function runPythonScript(scriptPath, args) {
  return new Promise((resolve, reject) => {
    const python = spawn('python', [scriptPath, ...args]);
    
    let output = '';
    python.stdout.on('data', (data) => {
      output += data.toString();
    });
    
    python.on('close', (code) => {
      if (code === 0) {
        resolve(JSON.parse(output));
      } else {
        reject(new Error(`Python script failed: ${code}`));
      }
    });
  });
}

// 3. Background job processing
class JobProcessor {
  constructor(maxWorkers = 4) {
    this.maxWorkers = maxWorkers;
    this.workers = [];
    this.queue = [];
  }
  
  async processJob(jobData) {
    return new Promise((resolve, reject) => {
      const job = { data: jobData, resolve, reject };
      
      if (this.workers.length < this.maxWorkers) {
        this.startWorker(job);
      } else {
        this.queue.push(job);
      }
    });
  }
  
  startWorker(job) {
    const worker = fork('./job-worker.js');
    this.workers.push(worker);
    
    worker.send(job.data);
    
    worker.on('message', (result) => {
      job.resolve(result);
      this.removeWorker(worker);
      this.processQueue();
    });
    
    worker.on('error', (error) => {
      job.reject(error);
      this.removeWorker(worker);
      this.processQueue();
    });
  }
  
  removeWorker(worker) {
    const index = this.workers.indexOf(worker);
    if (index !== -1) {
      this.workers.splice(index, 1);
    }
  }
  
  processQueue() {
    if (this.queue.length > 0) {
      const job = this.queue.shift();
      this.startWorker(job);
    }
  }
}

// When to use each method:
// - exec(): Simple commands with small output
// - execFile(): Running binaries, more secure
// - spawn(): Large output, streaming, real-time data
// - fork(): Node.js modules, IPC needed
```

**[⬆ Back to Top](#table-of-contents)**

### 58. How do you handle backpressure in streams?

Backpressure handling is crucial for preventing memory issues when processing large amounts of data.

```javascript
const fs = require('fs');
const { Transform, pipeline } = require('stream');

// ❌ WRONG - Ignoring backpressure
function badStreamHandling() {
  const readStream = fs.createReadStream('large-file.txt');
  const writeStream = fs.createWriteStream('output.txt');
  
  readStream.on('data', (chunk) => {
    // Ignoring return value - potential memory issue
    writeStream.write(chunk);
  });
}

// ✅ CORRECT - Manual backpressure handling
function goodStreamHandling() {
  const readStream = fs.createReadStream('large-file.txt');
  const writeStream = fs.createWriteStream('output.txt');
  
  readStream.on('data', (chunk) => {
    const canContinue = writeStream.write(chunk);
    
    if (!canContinue) {
      // Buffer is full, pause reading
      readStream.pause();
    }
  });
  
  writeStream.on('drain', () => {
    // Buffer is drained, resume reading
    readStream.resume();
  });
  
  readStream.on('end', () => {
    writeStream.end();
  });
}

// ✅ BEST - Using pipe (handles backpressure automatically)
function bestStreamHandling() {
  const readStream = fs.createReadStream('large-file.txt');
  const writeStream = fs.createWriteStream('output.txt');
  
  readStream.pipe(writeStream);
}

// ✅ EXCELLENT - Using pipeline (better error handling)
function excellentStreamHandling() {
  pipeline(
    fs.createReadStream('large-file.txt'),
    fs.createWriteStream('output.txt'),
    (err) => {
      if (err) {
        console.error('Pipeline failed:', err);
      } else {
        console.log('Pipeline succeeded');
      }
    }
  );
}

// Custom Transform stream with backpressure
class ThrottledTransform extends Transform {
  constructor(options) {
    super(options);
    this.delay = options.delay || 0;
  }
  
  _transform(chunk, encoding, callback) {
    // Simulate slow processing
    setTimeout(() => {
      this.push(chunk.toString().toUpperCase());
      callback(); // Signal that we're ready for more data
    }, this.delay);
  }
}

// Using throttled transform
pipeline(
  fs.createReadStream('input.txt'),
  new ThrottledTransform({ delay: 10 }),
  fs.createWriteStream('output.txt'),
  (err) => {
    if (err) console.error(err);
  }
);

// Monitoring backpressure
class MonitoredWriteStream extends Transform {
  constructor(options) {
    super(options);
    this.backpressureCount = 0;
  }
  
  _transform(chunk, encoding, callback) {
    const canWrite = this.push(chunk);
    
    if (!canWrite) {
      this.backpressureCount++;
      console.log(`Backpressure occurred ${this.backpressureCount} times`);
    }
    
    callback();
  }
}

// HTTP response streaming with backpressure
const http = require('http');

http.createServer((req, res) => {
  const stream = fs.createReadStream('large-video.mp4');
  
  stream.on('data', (chunk) => {
    const canContinue = res.write(chunk);
    
    if (!canContinue) {
      stream.pause();
      res.once('drain', () => {
        stream.resume();
      });
    }
  });
  
  stream.on('end', () => {
    res.end();
  });
  
  stream.on('error', (err) => {
    res.statusCode = 500;
    res.end('Error reading file');
  });
}).listen(3000);

// Better: Using pipe
http.createServer((req, res) => {
  const stream = fs.createReadStream('large-video.mp4');
  stream.pipe(res);
}).listen(3000);

// Database streaming with backpressure
const { Readable } = require('stream');

class DatabaseStream extends Readable {
  constructor(query, options) {
    super({ objectMode: true, ...options });
    this.query = query;
    this.offset = 0;
    this.limit = 100;
    this.done = false;
  }
  
  async _read() {
    if (this.done) return;
    
    try {
      const results = await this.query
        .limit(this.limit)
        .offset(this.offset)
        .exec();
      
      if (results.length === 0) {
        this.done = true;
        this.push(null); // Signal end of stream
        return;
      }
      
      this.offset += results.length;
      
      for (const row of results) {
        const canContinue = this.push(row);
        if (!canContinue) {
          // Backpressure - wait for _read to be called again
          return;
        }
      }
    } catch (err) {
      this.destroy(err);
    }
  }
}

// Usage
const dbStream = new DatabaseStream(User.find());

pipeline(
  dbStream,
  new Transform({
    objectMode: true,
    transform(user, encoding, callback) {
      // Process each user
      const processed = processUser(user);
      callback(null, JSON.stringify(processed) + '\n');
    }
  }),
  fs.createWriteStream('users.json'),
  (err) => {
    if (err) console.error('Export failed:', err);
    else console.log('Export completed');
  }
);

// Handling backpressure in custom streams
class CustomWritableStream extends require('stream').Writable {
  constructor() {
    super();
    this.buffer = [];
    this.processing = false;
  }
  
  _write(chunk, encoding, callback) {
    this.buffer.push(chunk);
    
    if (!this.processing) {
      this.processBuffer();
    }
    
    // Signal backpressure if buffer is too large
    if (this.buffer.length > 100) {
      this.once('drained', callback);
    } else {
      callback();
    }
  }
  
  async processBuffer() {
    this.processing = true;
    
    while (this.buffer.length > 0) {
      const chunk = this.buffer.shift();
      await this.processChunk(chunk);
      
      if (this.buffer.length === 0) {
        this.emit('drained');
      }
    }
    
    this.processing = false;
  }
  
  async processChunk(chunk) {
    // Simulate async processing
    return new Promise(resolve => {
      setTimeout(() => {
        console.log('Processed:', chunk.length, 'bytes');
        resolve();
      }, 100);
    });
  }
}
```

**[⬆ Back to Top](#table-of-contents)**

### 59. What is garbage collection in Node.js?

Garbage Collection (GC) is the process of automatically freeing memory that is no longer being used. Node.js uses V8's garbage collector.

**V8 Garbage Collection:**
- **Minor GC (Scavenge)**: Collects young generation objects
- **Major GC (Mark-Sweep-Compact)**: Collects old generation objects

```javascript
// Understanding memory spaces
// Young Generation: New objects (fast GC)
// Old Generation: Long-lived objects (slower GC)

// Monitoring garbage collection
const v8 = require('v8');

// Get heap statistics
function getHeapStats() {
  const stats = v8.getHeapStatistics();
  return {
    totalHeapSize: `${(stats.total_heap_size / 1024 / 1024).toFixed(2)} MB`,
    usedHeapSize: `${(stats.used_heap_size / 1024 / 1024).toFixed(2)} MB`,
    heapSizeLimit: `${(stats.heap_size_limit / 1024 / 1024).toFixed(2)} MB`,
    mallocedMemory: `${(stats.malloced_memory / 1024 / 1024).toFixed(2)} MB`
  };
}

console.log(getHeapStats());

// Force garbage collection (requires --expose-gc flag)
// node --expose-gc app.js
if (global.gc) {
  global.gc();
  console.log('Garbage collection triggered');
}

// Get heap space statistics
function getHeapSpaceStats() {
  return v8.getHeapSpaceStatistics().map(space => ({
    name: space.space_name,
    size: `${(space.space_size / 1024 / 1024).toFixed(2)} MB`,
    used: `${(space.space_used_size / 1024 / 1024).toFixed(2)} MB`,
    available: `${(space.space_available_size / 1024 / 1024).toFixed(2)} MB`
  }));
}

console.log(getHeapSpaceStats());

// Understanding GC triggers
// 1. Allocation failure in young generation -> Minor GC
// 2. Old generation reaching threshold -> Major GC
// 3. Manual trigger with global.gc()

// GC-friendly coding patterns

// ❌ BAD - Creates garbage
function createGarbage() {
  for (let i = 0; i < 1000000; i++) {
    const temp = { data: new Array(100) };
    // temp becomes garbage immediately
  }
}

// ✅ GOOD - Reuse objects
function reuseObjects() {
  const reusable = { data: new Array(100) };
  for (let i = 0; i < 1000000; i++) {
    reusable.data.fill(i);
    // Same object reused
  }
}

// Object pooling to reduce GC pressure
class ObjectPool {
  constructor(createFn, resetFn, initialSize = 10) {
    this.createFn = createFn;
    this.resetFn = resetFn;
    this.pool = [];
    
    for (let i = 0; i < initialSize; i++) {
      this.pool.push(createFn());
    }
  }
  
  acquire() {
    if (this.pool.length > 0) {
      return this.pool.pop();
    }
    return this.createFn();
  }
  
  release(obj) {
    this.resetFn(obj);
    this.pool.push(obj);
  }
}

// Usage
const bufferPool = new ObjectPool(
  () => Buffer.allocUnsafe(1024),
  (buf) => buf.fill(0),
  50
);

function processData(data) {
  const buffer = bufferPool.acquire();
  // Use buffer
  bufferPool.release(buffer);
}

// Monitoring GC performance
const { PerformanceObserver, performance } = require('perf_hooks');

const obs = new PerformanceObserver((list) => {
  const entries = list.getEntries();
  entries.forEach((entry) => {
    if (entry.entryType === 'gc') {
      console.log(`GC ${entry.kind === 1 ? 'Scavenge' : 'Mark-Sweep-Compact'}`);
      console.log(`Duration: ${entry.duration.toFixed(2)}ms`);
    }
  });
});

obs.observe({ entryTypes: ['gc'] });

// V8 flags for GC tuning
// node --max-old-space-size=4096 app.js (increase heap size)
// node --max-semi-space-size=64 app.js (young generation size)
// node --expose-gc app.js (enable manual GC)
// node --trace-gc app.js (log GC events)
// node --trace-gc-verbose app.js (detailed GC logs)

// Detecting memory issues
class MemoryMonitor {
  constructor(interval = 5000) {
    this.interval = interval;
    this.measurements = [];
    this.maxMeasurements = 100;
  }
  
  start() {
    this.timer = setInterval(() => {
      const usage = process.memoryUsage();
      
      this.measurements.push({
        timestamp: Date.now(),
        heapUsed: usage.heapUsed,
        heapTotal: usage.heapTotal,
        rss: usage.rss
      });
      
      if (this.measurements.length > this.maxMeasurements) {
        this.measurements.shift();
      }
      
      this.checkForLeaks();
    }, this.interval);
  }
  
  checkForLeaks() {
    if (this.measurements.length < 10) return;
    
    const recent = this.measurements.slice(-10);
    const trend = recent.reduce((sum, m) => sum + m.heapUsed, 0) / recent.length;
    const oldest = this.measurements[0];
    
    const growth = ((trend - oldest.heapUsed) / oldest.heapUsed) * 100;
    
    if (growth > 50) {
      console.warn(`Potential memory leak detected: ${growth.toFixed(2)}% growth`);
    }
  }
  
  stop() {
    if (this.timer) {
      clearInterval(this.timer);
    }
  }
  
  getStats() {
    const latest = this.measurements[this.measurements.length - 1];
    return {
      heapUsed: `${(latest.heapUsed / 1024 / 1024).toFixed(2)} MB`,
      heapTotal: `${(latest.heapTotal / 1024 / 1024).toFixed(2)} MB`,
      rss: `${(latest.rss / 1024 / 1024).toFixed(2)} MB`
    };
  }
}

const monitor = new MemoryMonitor();
monitor.start();

// Best practices for GC optimization:
// 1. Avoid creating unnecessary objects
// 2. Use object pooling for frequently created objects
// 3. Clear large data structures when done
// 4. Use WeakMap/WeakSet for caches
// 5. Implement proper cleanup in destructors
// 6. Monitor memory usage in production
// 7. Use streaming for large datasets
// 8. Avoid closures holding large objects
```

**[⬆ Back to Top](#table-of-contents)**

### 60. What are V8 flags and how to use them?

V8 flags allow you to configure and optimize the V8 JavaScript engine's behavior.

```javascript
// Common V8 flags

// 1. Memory management
// node --max-old-space-size=4096 app.js
// Increase heap size to 4GB (default: ~1.4GB on 64-bit)

// node --max-semi-space-size=64 app.js
// Set young generation size to 64MB

// 2. Garbage collection
// node --expose-gc app.js
// Enable manual garbage collection via global.gc()

// node --trace-gc app.js
// Log GC events
// Output: [12345:0x...] 25 ms: Scavenge 2.6 (3.0) -> 1.8 (3.0) MB

// node --trace-gc-verbose app.js
// Detailed GC logging

// node --gc-interval=100 app.js
// Set GC interval

// 3. Performance profiling
// node --prof app.js
// Generate v8.log profiling data

// Process the log:
// node --prof-process isolate-*.log > processed.txt

// node --trace-opt app.js
// Log optimized functions

// node --trace-deopt app.js
// Log deoptimized functions

// 4. Debugging
// node --inspect app.js
// Enable Chrome DevTools debugging

// node --inspect-brk app.js
// Break before user code starts

// node --trace-warnings app.js
// Show stack traces for warnings

// 5. Optimization flags
// node --optimize-for-size app.js
// Optimize for memory usage

// node --always-turbofan app.js
// Always use TurboFan compiler (aggressive optimization)

// node --no-turbo-inlining app.js
// Disable function inlining

// Using flags programmatically
const v8 = require('v8');

// Set flags before they take effect
v8.setFlagsFromString('--max-old-space-size=4096');

// Get V8 version
console.log(process.versions.v8);

// Heap statistics
console.log(v8.getHeapStatistics());

// Heap snapshot
const fs = require('fs');
const snapshotStream = v8.getHeapSnapshot();
const fileName = `heap-${Date.now()}.heapsnapshot`;
const fileStream = fs.createWriteStream(fileName);
snapshotStream.pipe(fileStream);

// Serialize and deserialize
const obj = { a: 1, b: 'test', c: [1, 2, 3] };
const serialized = v8.serialize(obj);
const deserialized = v8.deserialize(serialized);

// Real-world examples

// 1. High-memory application
// package.json
{
  "scripts": {
    "start": "node --max-old-space-size=8192 app.js"
  }
}

// 2. Production monitoring
// pm2 ecosystem.config.js
module.exports = {
  apps: [{
    name: 'app',
    script: './app.js',
    node_args: [
      '--max-old-space-size=4096',
      '--trace-warnings',
      '--trace-gc'
    ]
  }]
};

// 3. Development debugging
// .vscode/launch.json
{
  "version": "0.2.0",
  "configurations": [{
    "type": "node",
    "request": "launch",
    "name": "Launch Program",
    "program": "${workspaceFolder}/app.js",
    "runtimeArgs": [
      "--expose-gc",
      "--trace-warnings"
    ]
  }]
}

// 4. Performance testing
class PerformanceTester {
  static testWithFlags(flags, testFn) {
    const { spawnSync } = require('child_process');
    
    const result = spawnSync('node', [
      ...flags,
      '-e',
      `(${testFn.toString()})()`
    ]);
    
    return {
      stdout: result.stdout.toString(),
      stderr: result.stderr.toString(),
      status: result.status
    };
  }
}

// Usage
const result = PerformanceTester.testWithFlags(
  ['--trace-opt', '--trace-deopt'],
  () => {
    function hotFunction(x) {
      return x * 2 + 1;
    }
    
    for (let i = 0; i < 100000; i++) {
      hotFunction(i);
    }
  }
);

console.log(result.stderr); // Shows optimization info

// 5. Memory leak detection
function detectMemoryLeak() {
  const v8 = require('v8');
  const fs = require('fs');
  
  // Take initial snapshot
  const snapshot1 = v8.writeHeapSnapshot();
  console.log('Snapshot 1:', snapshot1);
  
  // Run your application
  runApplication();
  
  // Take second snapshot
  const snapshot2 = v8.writeHeapSnapshot();
  console.log('Snapshot 2:', snapshot2);
  
  console.log('Compare snapshots in Chrome DevTools');
}

// Environment-specific flags
const isDevelopment = process.env.NODE_ENV === 'development';
const flags = [];

if (isDevelopment) {
  flags.push('--expose-gc');
  flags.push('--trace-warnings');
} else {
  flags.push('--max-old-space-size=4096');
  flags.push('--optimize-for-size');
}

// Set flags
if (flags.length > 0) {
  v8.setFlagsFromString(flags.join(' '));
}

// Checking available flags
// node --v8-options | grep -i gc
// Lists all GC-related flags

// Common flag combinations:

// Development:
// node --inspect --trace-warnings --expose-gc app.js

// Production:
// node --max-old-space-size=4096 --optimize-for-size app.js

// Performance testing:
// node --prof --trace-opt --trace-deopt app.js

// Memory debugging:
// node --expose-gc --trace-gc --trace-gc-verbose app.js

// Best practices:
// 1. Don't use --expose-gc in production
// 2. Tune --max-old-space-size based on available RAM
// 3. Use profiling flags only for debugging
// 4. Monitor GC logs in production
// 5. Test with different flag combinations
// 6. Document flags in package.json scripts
```

**[⬆ Back to Top](#table-of-contents)**

### 61. How do you create a REST API with Express.js?

A REST API exposes resources through HTTP methods and predictable URLs. For example, a product catalog can use `GET /api/products` to list products, `GET /api/products/:id` to retrieve one, `POST /api/products` to create one, `PATCH /api/products/:id` to update fields, and `DELETE /api/products/:id` to remove one.

```javascript
const express = require('express');

const app = express();
app.use(express.json());

// In production, persist records in a database through a repository/service.
const products = new Map();
let nextId = 1;

app.get('/api/products', (req, res) => {
  res.json([...products.values()]);
});

app.get('/api/products/:id', (req, res) => {
  const product = products.get(req.params.id);
  if (!product) {
    return res.status(404).json({ error: { code: 'NOT_FOUND', message: 'Product not found' } });
  }
  return res.json(product);
});

app.post('/api/products', (req, res) => {
  const { name, price } = req.body ?? {};
  if (typeof name !== 'string' || !name.trim() ||
      typeof price !== 'number' || price < 0) {
    return res.status(400).json({
      error: { code: 'VALIDATION_ERROR', message: 'A name and non-negative numeric price are required' }
    });
  }

  const product = { id: String(nextId++), name: name.trim(), price };
  products.set(product.id, product);
  return res.status(201)
    .location(`/api/products/${product.id}`)
    .json(product);
});

app.patch('/api/products/:id', (req, res) => {
  const product = products.get(req.params.id);
  if (!product) {
    return res.status(404).json({ error: { code: 'NOT_FOUND', message: 'Product not found' } });
  }

  const changes = req.body ?? {};
  if (Object.hasOwn(changes, 'name') &&
      (typeof changes.name !== 'string' || !changes.name.trim())) {
    return res.status(400).json({
      error: { code: 'VALIDATION_ERROR', message: 'Name must be a non-empty string' }
    });
  }
  if (Object.hasOwn(changes, 'price') &&
      (typeof changes.price !== 'number' || changes.price < 0)) {
    return res.status(400).json({
      error: { code: 'VALIDATION_ERROR', message: 'Price must be a non-negative number' }
    });
  }

  const updated = {
    ...product,
    ...(Object.hasOwn(changes, 'name') ? { name: changes.name.trim() } : {}),
    ...(Object.hasOwn(changes, 'price') ? { price: changes.price } : {})
  };
  products.set(product.id, updated);
  return res.json(updated);
});

app.delete('/api/products/:id', (req, res) => {
  if (!products.has(req.params.id)) {
    return res.status(404).json({ error: { code: 'NOT_FOUND', message: 'Product not found' } });
  }
  products.delete(req.params.id);
  return res.status(204).end();
});
```

In a production API, keep route handlers thin: move business rules into a service, persistence into a repository, validate all inputs with a schema or DTO, and add authentication, authorization, logging, and tests.

**[⬆ Back to Top](#table-of-contents)**

### 62. How do you validate API requests and handle errors in Express.js?

Validate untrusted input at the API boundary and return a stable error shape. Use `400 Bad Request` for invalid input, `401 Unauthorized` for missing/invalid authentication, `403 Forbidden` when an authenticated caller lacks permission, `404 Not Found` for missing resources, and `500 Internal Server Error` for unexpected failures. Do not send stack traces or internal details to clients.

```javascript
app.use((err, req, res, next) => {
  if (res.headersSent) return next(err);

  console.error(err);
  return res.status(err.statusCode || 500).json({
    error: {
      code: err.code || 'INTERNAL_ERROR',
      message: err.statusCode ? err.message : 'An unexpected error occurred'
    }
  });
});
```

For example, a `POST /api/orders` endpoint should reject an empty item list or invalid quantities before writing to the database. A schema-validation library can produce field-level messages; pass unexpected errors to the centralized middleware with `next(error)` so every route responds consistently.

**[⬆ Back to Top](#table-of-contents)**

### 63. How do you add pagination and filtering to an API?

Accept bounded query parameters, validate them, and return page metadata alongside the results. For a product catalog, a client might request `/api/products?category=books&page=2&limit=20`.

```javascript
app.get('/api/products', async (req, res, next) => {
  try {
    const page = Math.max(1, Number.parseInt(req.query.page, 10) || 1);
    const limit = Math.min(100, Math.max(1, Number.parseInt(req.query.limit, 10) || 20));
    const category = typeof req.query.category === 'string' ? req.query.category : undefined;

    const result = await productService.list({ category, page, limit });
    return res.json({
      items: result.items,
      page,
      limit,
      total: result.total
    });
  } catch (error) {
    return next(error);
  }
});
```

Apply filtering and pagination in the database rather than loading the full collection into memory. Offset pagination is simple for numbered pages; cursor pagination is usually more stable for large or frequently changing datasets.

**[⬆ Back to Top](#table-of-contents)**

---

## Contributing

Feel free to contribute by submitting pull requests to add more questions or improve existing answers.


---

## Folder Description

This folder contains Node.js interview questions and answers covering Node.js runtime, event loop, modules, streams, file system, Express.js, and other server-side JavaScript development topics.

**[⬅ Return to Root README](../README.md)**
