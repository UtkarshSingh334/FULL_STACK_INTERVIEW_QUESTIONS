# 🟢 Express & Node.js - Hard Questions From Notes

> **Topics from Notes Covered:** Libuv Details Explanation, `process.nextTick` (`process.next`), Buffer and Cluster, Streams & Backpressure, Streams/fs/threads in Node.js vs React Native.

---

### Q1: Libuv Detailed Explanation (Event Loop Phases & Thread Pool)
**Question (From Notes):** Give a detailed explanation of Libuv, the 6 Event Loop phases, and the background Thread Pool.

**Answer:**
Libuv is a C library providing Node.js with its event-driven asynchronous I/O engine.

```
   ┌───────────────────────────┐
┌─>│          timers           │  -> setTimeout() & setInterval() callbacks
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     pending callbacks     │  -> Deferred I/O callbacks from previous cycle
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare       │  -> Internal Libuv usage only
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           poll            │  -> Fetch new I/O events (network & disk reads)
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           check           │  -> setImmediate() callbacks
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │      close callbacks      │  -> socket.on('close') events
└──┴───────────────────────────┘
```

**Libuv Thread Pool (`UV_THREADPOOL_SIZE`):**
- Asynchronous tasks in JavaScript run on a single main thread.
- Blocking operations (`fs` file system calls, `crypto` hashing, `zlib` compression, DNS lookups) are delegated by Libuv to a background worker thread pool (defaults to **4 threads**).
- Can be tuned before process starts: `UV_THREADPOOL_SIZE=8 node app.js`.
- Network I/O is non-blocking and uses OS kernel event notification mechanisms (`epoll`/`kqueue`/`IOCP`) without touching the thread pool.

---

### Q2: `process.nextTick` (`process.next`)
**Question (From Notes):** Explain `process.nextTick()` and how it prioritizes against `setImmediate` and `setTimeout`.

**Answer:**
- **`process.nextTick()`** has the **highest priority** in Node.js. It runs in the microtask queue immediately after the current operation completes, before the event loop advances to any other phase or microtask.
- **`Promise.then()`**: Runs in the microtask queue right after `process.nextTick`.
- **`setTimeout(fn, 0)`**: Evaluated in Timers phase.
- **`setImmediate(fn)`**: Evaluated in Check phase.

```javascript
console.log("1. Sync Start");

setTimeout(() => console.log("6. setTimeout"), 0);
setImmediate(() => console.log("7. setImmediate"));

Promise.resolve().then(() => console.log("4. Promise Microtask"));
process.nextTick(() => console.log("3. process.nextTick (Top Priority)"));

console.log("2. Sync End");

// Output Order:
// 1. Sync Start -> 2. Sync End -> 3. process.nextTick -> 4. Promise -> 6. setTimeout -> 7. setImmediate
```

---

### Q3: Buffer and Cluster in Node.js
**Question (From Notes):** Explain Buffer and Cluster in Node.js.

**Answer:**
- **Buffer**: Allocates raw binary memory **outside the V8 garbage-collected heap** directly via C++ Libuv layer. Used to handle binary streams (files, network packets, images) without triggering V8 GC pauses.
  ```javascript
  const buf = Buffer.from("NodeJS", "utf8");
  console.log(buf); // <Buffer 4e 6f 64 65 4a 53>
  ```
- **Cluster**: Allows spawning multiple worker Node.js processes across multi-core CPUs that all share the same server TCP port, achieving horizontal multi-process scaling.
  ```javascript
  const cluster = require('cluster');
  const http = require('http');
  const os = require('os');

  if (cluster.isPrimary) {
    const numCPUs = os.cpus().length;
    for (let i = 0; i < numCPUs; i++) cluster.fork();
  } else {
    http.createServer((req, res) => res.end(`Worker PID: ${process.pid}\n`)).listen(3000);
  }
  ```

---

### Q4: Node.js Streams & Backpressure
**Question (From Notes):** What are Streams, and what is Backpressure?

**Answer:**
Streams process data sequentially in small chunks without loading the entire file into RAM.
- **4 Types**: `Readable`, `Writable`, `Duplex`, `Transform`.
- **Backpressure**: Occurs when the readable stream reads data faster than the writable stream can write it. `stream.pipeline` automatically handles backpressure and frees resources.

```javascript
const fs = require('fs');
const zlib = require('zlib');
const { pipeline } = require('stream/promises');

async function compressStream(src, dest) {
  await pipeline(
    fs.createReadStream(src),
    zlib.createGzip(),
    fs.createWriteStream(dest)
  );
  console.log("Compressed stream safely!");
}
```
