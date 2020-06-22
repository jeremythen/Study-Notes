

# You don't know Node notes

The Nodejs Event Queue lives in a library called 'libuv'. Not part of V8.

The heap and the stack are part of V8.


Set timeout is not Javascript. In node, it's a node API. In the browser, it's a browser API.

When the event loop and the stack are empty, node will exit.

Other nodes libraries besides V8 and libuv: http-parser, c-ares, OpenSSL, zlib. They are external to node.

Node can run without V8, it can run with Chakra.


Exporting:
module.exports.g = 42;
exports.g = 42;
---


The objects exports, require and module are globally available in every file but they are different in every file.

Nodes magic IIFE:

[(function (exports, require, module, __filename, __dirname))...]



5 major steps when you require a module:

1) Resolving, trying to map the string into a path to find the module.
2) Loading, the content of the file into memory
3) Wrapping that content into an IIFE
4) Evaluating
5) Caching, se next time, it will not do the previous steps, but simply use the cached content.

---

Checking if the module exists:

```javascript
require.resolve("module-name");
```

Circular modular dependencies in node?

module2 requires module1, and module1 requires module2.
This doesn't throw an error. The modules get a partial version of the other. Avoid this.

---

What are the 3 extensions that require will try to find?

require('./module)

.js, then json, then .node


---


What are the major differences between spawn and exec?

They both allow you to run commands in the operating system.

spawn does not use a shell by default. And uses streams.
exec uses shell. Uses buffer output.

spawn is better to use. Using shell is not that secure. Buffers will load the whole content, steams will load the content as it needs.

---

How to make node always use Javascript strict mode?

run command:

> node --use-strict

---

What is process.argv?

It shows the arguments passed to node when started.

--- 

How can we do an do a final action if node crashes?
Always use this in your software:
process.on('uncaughtException', err => {
    fs.writeSync(1, 'an exception');
    process.exit(1); // not optional. Always exit.
});

Always make sync operations with this, since the event queue it's already done and may not work properly.

---

What are the . commands that can be used?

.help
.break  sometimes you get stuck, this gets you out
.clear  Alias for .break
.editor Enter editor mode
.exit   Exit the repl
.load   Load JS from a file into the REPL session
.save   Save all evaluated commands in this REPL session to a file

---

What does the _ means inside of node REPL?

It returns the last executed value in the REPL.

> Math.random()
0.070053
> _
0.070053
> const a = _
undefined
> a
0.070053

---

Differences between Buffer.alloc and Buffer.allocUnsafe?

Buffer.alloc(34).toString() reads that portion of the memory and prints it and fills that range with zeros.

Buffer.allocUnsave.toString() reads that portion of the memory and prints it. Faster since it doesn't reset the memory, which means that you could read data that was already there.

---

What is the cluster module?

You have the master process inside the server, and that master process forks a few workers to handle those requests.
Node by default does a Round Robin algorithm.

Each thread have their own memory, V8 instance, etc. So they cannot communicate with each other and cache data they they can all use.

---

When is it ok to use the file system Sync methods?

When first initializing, it can be ok to do sync operations.
But when not, doing sync operations will block the event loop and no body else will move further until that process finishes.

---

How can you print the first level of an object?

console.dir(object, { depth: 0 });

---

How to reset Node in Chrome dev-tools?

node --inspect

---

Asynchrony

Are callbacks synchronous. yes.
Callbbacks don't indicate Asynchrony.
Callsbacks can be both sync o async. So, you should have all your functions either or, but not both.

---

Event Emitters

const EventEmitters = require('events');

class Logger extends EventEmitters {}

const logger = new Logger();

logger.emit('event');

logger.on('event', myListenerFunc);


This is specially good when you want to have multiple callbacks, multiple things to be able to register to this. Better than normal callbacks in this case.

---

Example of a built-in stream in Node that is both readable and writable?

crypto.createCipher
zlib.createGzip

Steams are really important in Node. 'If you are not using streams, you are doing it wrong'.

---

Streams

Streams are a collection of data that might not be available all at once and don't have to fit in memory.

There are 4 types of steams:

1) Readable (fs.createReadStream)
2) Writable (fs.createWriteStream)
3) Duplex (read and write, net.socket)
4) Transform (like the zlib library)

All streams are EventEmitters

**readable.pipe(writable);**

Readable streams can be paused.

Paused:
stream.read()

Flowing
EventEmitter

Everything is node is a stream:

Readable streams:
HTTP responses, requests, fs read, zlib, crypto, TCP sockets, child process stdout and stderr, process.stdin.

Writable steams:

HTTP responses, requests, fs write, zlib, crypto, TCP, child process stdin, process.stdout, process.stderr.


You can implement streams, importing require('stream');
Or simply consume it: piping/events

---

Global

global.module
global.require()
global.filename
global.process
global.argc


process.args
process.argv
process.env
process.uptime()
process.memoryUsage()
process.exit()
process.kill()

process.stdin

etc.

Events === Nodes Observer Pattern

---

setImmediate(fn) is faster than setTimeout. Executes after IO/Events. setTimeout executes after the queue empties.

clearImmediate(immediate)

setImmediate(console.log.bind(null, 'log 1')); setImmediate(console.log.bind(null, 'log 2')); setImmediate(console.log.bind(null, 'log 3')); setImmediate(console.log.bind(null, 'log 4'));

setTimeout(console.log.bind(null, 'log 1')); setTimeout(console.log.bind(null, 'log 2')); setTimeout(console.log.bind(null, 'log 3')); setTimeout(console.log.bind(null, 'log 4'));

---

How to avoid callback hell?

You can separate each call in multiple functions, that helps.

You can also use Promises.

You can finally use async/await.

---

How do you handle threads in nodejs?

You basically don't. The thread available to the developer is the main thread. But node can spawn child threads.

---

There is a pattern in node that passes an error object as the first argument of a callback to handle errors first.

---

console.time('mytime');
// some long operation
console.timeEnd('loop');

---

Declaring a variable with var in the browser, attaches it to the big window object.
Declaring a variable with var in node, attaches it to the current module, which is smaller. This is faster.

---

REPL = READ, EVAL, PRINT, LOOP


---


Create a server:

```javascript

const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello, World!\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});

```

# Testing

The assert module provides a set of assertion functions for verifying invariants.

```javascript

const assert = require('assert').strict;

assert.deepEqual([[[1, 2, 3]], 4, 5], [[[1, 2, '3']], 4, 5]);

// AssertionError: Expected inputs to be strictly deep-equal. Due to the '3' and 3.

assert.deepEqual()
assert.equal()
assert.notDeepEqual()
assert.notEqual()

```

# child_process

## Using exec function

You can use it to execute a command in the shell.

The exec() function creates a new shell and executes a given command. The output from the execution is buffered, which means kept in memory, and is available for use in a callback.


```javascript
const { exec } = require("child_process");

exec("ls -la", (error, stdout, stderr) => {
    if (error) {
        console.log(`error: ${error.message}`);
        return;
    }
    if (stderr) {
        console.log(`stderr: ${stderr}`);
        return;
    }
    console.log(`stdout: ${stdout}`);
});

```


## Using spawn function

The spawn() function executes a command in a new process. This function uses a Stream API, so its output of the command is made available via listeners.

```javascript

const { spawn } = require("child_process");

const ls = spawn("ls", ["-la"]);

ls.stdout.on("data", data => {
    console.log(`stdout: ${data}`);
});

ls.stderr.on("data", data => {
    console.log(`stderr: ${data}`);
});

ls.on('error', (error) => {
    console.log(`error: ${error.message}`);
});

ls.on("close", code => {
    console.log(`child process exited with code ${code}`);
});

```

## spawn, exec, fork

```javascript
const { spawn } = require('child_process');
const bat = spawn('cmd.exe', ['/c', 'my.bat']);

bat.stdout.on('data', (data) => {
  console.log(data.toString());
});

bat.stderr.on('data', (data) => {
  console.error(data.toString());
});

bat.on('exit', (code) => {
  console.log(`Child exited with code ${code}`);
});

// OR...
const { exec, spawn } = require('child_process');
exec('my.bat', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(stdout);
});

// Script with spaces in the filename:
const bat = spawn('"my script.cmd"', ['a', 'b'], { shell: true });
// or:
exec('"my script.cmd" a b', (err, stdout, stderr) => {
  // ...
});


const { fork } = require('child_process');

const forked = fork('child.js');

forked.on('message', (msg) => {
  console.log('Message from child', msg);
});

forked.send({ hello: 'world' });


```


## When to use exec and spawn?

The key difference between exec() and spawn() is how they return the data. As exec() stores all the output in a buffer, it is more memory intensive than spawn(), which streams the output as it comes.

Conclusion

Node.js can run shell commands by using the standard child_process module. If we use the exec() function, our command will run and its output will be available to us in a callback. If we use the spawn() module, its output will be available via event listeners.

If our application expects a lot of output from our commands, we should prefer spawn() over exec(). If not, we might opt to use exec() for its simplicity.

The importance of the distinction between child_process.exec() and child_process.execFile() can vary based on platform. On Unix-type operating systems (Unix, Linux, macOS) child_process.execFile() can be more efficient because it does not spawn a shell by default. On Windows, however, .bat and .cmd files are not executable on their own without a terminal, and therefore cannot be launched using child_process.execFile().

With fork, a process can create a child process and communicate with it through messages, using EventEmitters.

---

# Cluster

The worker processes are spawned using the child_process.fork() method, so that they can communicate with the parent via IPC and pass server handles back and forth.

```javascript
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
  console.log(`Master ${process.pid} is running`);

  // Fork workers.
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  cluster.on('exit', (worker, code, signal) => {
    console.log(`worker ${worker.process.pid} died`);
  });
} else {
  // Workers can share any TCP connection
  // In this case it is an HTTP server
  http.createServer((req, res) => {
    res.writeHead(200);
    res.end('hello world\n');
  }).listen(8000);

  console.log(`Worker ${process.pid} started`);
}

```

Because workers are all separate processes, they can be killed or re-spawned depending on a program's needs, without affecting other workers.

## Cluster notes

cluster.fork() returns a Worker object, which extends EventEmitter:

```javascript

for (let i = 0; i < numCPUs; i++) {
    
    const worker = cluster.fork();

    worker.on('disconnect', () => {
        // Worker has disconnected
    });

    worker.on('exit', (code, signal) => {})
}


for (const id in cluster.workers) {
    cluster.workers[id].on('message', messageHandler);
  }

  process.on('message', (msg) => {
    if (msg === 'shutdown') {
      // Initiate graceful close of any connections to server
    }
  });

  cluster.fork().on('online', () => {
  // Worker is online
});

cluster.on('exit', (worker, code, signal) => {
  if (worker.exitedAfterDisconnect === true) {
    console.log('Oh, it was just voluntary – no need to worry');
  }
});

// kill worker
worker.kill()


worker.isConnected()

worker.isDead()

cluster.on('fork', (worker) => {
    console.log('worker is dead:', worker.isDead());
});

worker.process

worker.send(message[, sendHandle[, options]][, callback])


```

You can also set all those events on the cluster itself.


---

# Using Console

```javascript

// const { Console } = require('console');
//  const { Console } = console;

const out = getStreamSomehow();
const err = getStreamSomehow();
const myConsole = new console.Console(out, err);

myConsole.log('hello world');
// Prints: hello world, to out
myConsole.log('hello %s', 'world');
// Prints: hello world, to out
myConsole.error(new Error('Whoops, something bad happened'));
// Prints: [Error: Whoops, something bad happened], to err

const name = 'Will Robinson';
myConsole.warn(`Danger ${name}! Danger!`);
// Prints: Danger Will Robinson! Danger!, to err

```


# Crypto

```javascript

const crypto = require('crypto');

const secret = 'abcdefg';
const hash = crypto.createHmac('sha256', secret)
                   .update('I love cupcakes')
                   .digest('hex');
console.log(hash);
// Prints:
//   c0fa1bc00531bd78ef38c628449c5102aeabd49b5dc3a2a516ea6ea959d6658e


```

# Debugging

> node inspect myscript.js

Use debugger keyword in .js files to have a break point.

---

# DNS

Use this module to get information about DNS, ip addresses, etc.

```javascript

const dns = require('dns');

dns.resolve4('archive.org', (err, addresses) => {
  if (err) throw err;

  console.log(`addresses: ${JSON.stringify(addresses)}`);

  addresses.forEach((a) => {
    dns.reverse(a, (err, hostnames) => {
      if (err) {
        throw err;
      }
      console.log(`reverse for ${a}: ${JSON.stringify(hostnames)}`);
    });
  });
});

dns.lookup('example.org', (err, address, family) => {
  console.log('address: %j family: IPv%s', address, family);
});

```

---

# ECMAScript Modules


```javascript

// Without ES
const state = require('./state.cjs');
module.exports.state = state;

// VS


// With ES
import state from './state.cjs';
export {
  state
};

```

# Events

```javascript

const EventEmitter = require('events');

class MyEmitter extends EventEmitter {}

const myEmitter = new MyEmitter();
myEmitter.on('event', () => {
  console.log('an event occurred!');
});
myEmitter.emit('event');

// Passing arguments and this to listeners

const myEmitter = new MyEmitter();
myEmitter.on('event', function(a, b) {
  console.log(a, b, this, this === myEmitter);
  // Prints:
  //   a b MyEmitter {
  //     domain: null,
  //     _events: { event: [Function] },
  //     _eventsCount: 1,
  //     _maxListeners: undefined } true
});
myEmitter.emit('event', 'a', 'b');



```

Asynchronous vs. Synchronous

The EventEmitter calls all listeners synchronously in the order in which they were registered. This ensures the proper sequencing of events and helps avoid race conditions and logic errors. When appropriate, listener functions can switch to an asynchronous mode of operation using the setImmediate() or process.nextTick() methods:


```javascript

const myEmitter = new MyEmitter();
myEmitter.on('event', (a, b) => {
  setImmediate(() => {
    console.log('this happens asynchronously');
  });
});
myEmitter.emit('event', 'a', 'b');


/// Using the eventEmitter.once() method, it is possible to register a listener that is called at most once for a particular event. Once the event is emitted, the listener is unregistered and then called.

const myEmitter = new MyEmitter();
let m = 0;
myEmitter.once('event', () => {
  console.log(++m);
});
myEmitter.emit('event');
// Prints: 1
myEmitter.emit('event');
// Ignored

///

myEmitter.emit('error', new Error('whoops!'));
myEmitter.on('error', (err) => {
  console.error('whoops! there was an error');
});


```

## Capture Rejections of Promises

he captureRejections option in the EventEmitter constructor or the global setting change this behavior, installing a .then(undefined, handler) handler on the Promise. This handler routes the exception asynchronously to the Symbol.for('nodejs.rejection') method if there is one, or to 'error' event handler if there is none.

```javascript

const ee1 = new EventEmitter({ captureRejections: true });
ee1.on('something', async (value) => {
  throw new Error('kaboom');
});

ee1.on('error', console.log);

const ee2 = new EventEmitter({ captureRejections: true });
ee2.on('something', async (value) => {
  throw new Error('kaboom');
});

ee2[Symbol.for('nodejs.rejection')] = console.log;

```

## Event: 'newListener'

The EventEmitter instance will emit its own 'newListener' event before a listener is added to its internal array of listeners.

```javascript

myEmitter.once('newListener', (event, listener) => {
  if (event === 'event') {
    // Insert a new listener in front
    myEmitter.on('event', () => {
      console.log('B');
    });
  }
});

```

# File System

All file system operations have synchronous and asynchronous forms.

const fs = require('fs');

The asynchronous form always takes a completion callback as its last argument. The arguments passed to the completion callback depend on the method, but the first argument is always reserved for an exception. If the operation was completed successfully, then the first argument will be null or undefined.


```javascript

fs.unlink('/tmp/hello', (err) => {
  if (err) throw err;
  console.log('successfully deleted /tmp/hello');
});


// There is no guaranteed ordering when using asynchronous methods. So the following is prone to error because the fs.stat() operation may complete before the fs.rename() operation:

fs.rename('/tmp/hello', '/tmp/world', (err) => {
  if (err) throw err;
  console.log('renamed complete');
});
fs.stat('/tmp/world', (err, stats) => {
  if (err) throw err;
  console.log(`stats: ${JSON.stringify(stats)}`);
});

// To correctly order the operations, move the fs.stat() call into the callback of the fs.rename() operation:

fs.rename('/tmp/hello', '/tmp/world', (err) => {
  if (err) throw err;
  fs.stat('/tmp/world', (err, stats) => {
    if (err) throw err;
    console.log(`stats: ${JSON.stringify(stats)}`);
  });
});

```

In busy processes, use the asynchronous versions of these calls. The synchronous versions will block the entire process until they complete, halting all connections. 


fs.open('/open/some/file.txt', 'r', (err, fd)...

fs.open(Buffer.from('/open/some/file.txt'), 'r', (err, fd) => {...



# Global Objects

Global Objects

* Class: Buffer
* __dirname
* __filename
* clearImmediate(immediateObject)
* clearInterval(intervalObject)
* clearTimeout(timeoutObject)
* console
* exports
* global
* module
* process
* queueMicrotask(callback)
* require()
* setImmediate(callback[, ...args])
* setInterval(callback, delay[, ...args])
* setTimeout(callback, delay[, ...args])
* TextDecoder
* TextEncoder
* URL
* URLSearchParams
* WebAssembly
* 

These objects are available in all modules. The following variables may appear to be global but are not. They exist only in the scope of modules, see the module system documentation:

* __dirname
* __filename
* exports
* module
* require()

---

# Modules

module.exports


The module.exports object is created by the Module system. Sometimes this is not acceptable; many want their module to be an instance of some class. To do this, assign the desired export object to module.exports. Assigning the desired object to exports will simply rebind the local exports variable, which is probably not what is desired.

```javascript
const EventEmitter = require('events');

module.exports = new EventEmitter();

// Do some work, and after some time emit
// the 'ready' event from the module itself.
setTimeout(() => {
  module.exports.emit('ready');
}, 1000);


///

const a = require('./a');
a.on('ready', () => {
  console.log('module "a" is ready');
});

// Assignment to module.exports must be done immediately. It cannot be done in any callbacks. This does not work:

setTimeout(() => {
  module.exports = { a: 'hello' };
}, 0);

```

# OS

The os module provides operating system-related utility methods and properties. It can be accessed using:

```javascript

const os = require('os');

os.cpus() // Returns all CPUs

```

# Path

The path module provides utilities for working with file and directory paths. It can be accessed using:

```javascript

const path = require('path');


// On Windows
path.basename('C:\\temp\\myfile.html');
// Returns: 'myfile.html'

//On POSIX and Windows:
path.win32.basename('C:\\temp\\myfile.html');
// Returns: 'myfile.html'

path.extname(path)

path.extname('index.html');
// Returns: '.html'

path.extname('index.coffee.md');
// Returns: '.md'

path.extname('index.');
// Returns: '.'

path.extname('index');
// Returns: ''

path.extname('.index');
// Returns: ''

path.extname('.index.md');
// Returns: '.md'


path.format({
  dir: 'C:\\path\\dir',
  base: 'file.txt'
});
// Returns: 'C:\\path\\dir\\file.txt'


```

# Process

The process object is a global that provides information about, and control over, the current Node.js process. As a global, it is always available to Node.js applications without using require(). It can also be explicitly accessed using require():


```javascript

const process = require('process');

process.on('beforeExit', (code) => {
  console.log('Process beforeExit event with code: ', code);
});

process.on('exit', (code) => {
  console.log('Process exit event with code: ', code);
});

console.log('This message is displayed first.');

// Prints:
// This message is displayed first.
// Process beforeExit event with code: 0
// Process exit event with code: 0

```

process.disconnect()

If the Node.js process is spawned with an IPC channel (see the Child Process and Cluster documentation), the process.disconnect() method will close the IPC channel to the parent process, allowing the child process to exit gracefully once there are no other connections keeping it alive.

The effect of calling process.disconnect() is the same as calling ChildProcess.disconnect() from the parent process.

---

# Stream

Streams can be readable, writable, or both. All streams are instances of EventEmitter.


```javascript

const stream = require('stream');

// The 'end' event indicates that the entire body has been received.
  req.on('end', () => {...


// Piping and unpiping

const writer = getWritableStreamSomehow();
const reader = getReadableStreamSomehow();
writer.on('unpipe', (src) => {
  console.log('Something has stopped piping into the writer.');
  assert.equal(src, reader);
});
reader.pipe(writer);
reader.unpipe(writer);



```
