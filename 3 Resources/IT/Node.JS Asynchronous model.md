---
up: 
related: "[[NodeJS]]"
created: 2025-05-02
---

Any JavaScript code you write in Node has to be placed in the call stack for V8 to execute it. The call stack is single-threaded, which means when there are functions in the call stack, everything else (including handler functions for asynchronous operations) will have to wait until the call stack is available again. That’s why it’s important to never write code that will keep the call stack busy (like a long-running for loop).

As long as the call stack is busy, all your asynchronous operation handlers will be waiting. Any code that needs to run for a long time should be executed outside of the main thread and its one call stack. While stacking functions in the call stack, when Node gets to an asynchronous task, it bypasses the call stack and processes the task internally. Depending on the nature of the task, Node might use a different thread or utilize the underlying OS asynchronous features.

Node uses the asynchronous features of its underlying OS to perform non-blocking I/O operations. For CPU-bound tasks and other tasks that can’t be handled asynchronously by the OS, Node provides a thread pool via its libuv library. This library is the backbone of everything asynchronous in Node

When an asynchronous task is completed, Node places its associated handler function in a queue structure known as the event queue (or task queue).

A queue is a first-in, first-out (FIFO) structure where the first thing added is the first one processed.

For a handler function to run, it needs to be placed on the call stack. That’s the job of the event loop. It’s a simple infinite loop with a simple job: when the event queue has handler functions and the call stack is empty, it picks the first queued function in the event queue and puts it on the call stack to have V8 execute it. Then it waits until the call stack is empty again to process the next queued handler function and keeps repeating that until there are no more handler functions in the event queue to process.

Another option to organize and use asynchronous code in Node is through the use of event emitter objects and event listener functions.

source: [[Efficient Node.JS]]