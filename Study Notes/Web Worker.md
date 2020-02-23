
# Parallel Computing in React

Parallel computing VS Concurrency

* Web Workers (Comlink)
* Web Assembly (AssemblyScript)
* Worklets (like a lite version of Web Worker)
* Service Worker 

## Terms:

Progressive Web Apps

---

You can use Web Workers for:

* Image manipulation and encoding
* Virtual DOM diffing
* Extensive calculation
* etc.

---

You have the main thread and the worker thread.

---

# COMLINK

comlink library to use Web Workder better.

```javascript
// importScript("comlinkurl");

const worker = new Worker("./worker.js");
const service = Comlink.proxy(worker); // Comlink.wrap(worker);
const value = await service.methodInWorker();
```

Use Web Workers to process work in the background without stopping the main thread, animations, etc.

