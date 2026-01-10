---
uuid: 20220717153618
created: 2022-07-17T15:36:18
alias: event demultiplexer
---

# [[Interface for Event Demultiplexer]]

Each operating system has its own interface for the event demultiplexer: **`epoll`** on Linux, **`kqueue`** on macOS, and the I/O completion port (**`IOCP`**) API on Windows. On top of that, each I/O operation can behave quite differently depending on the type of resource, even within the same operating system. In Unix operating systems, for example, regular filesystem **files do not support non-blocking operations**, so in order to simulate non-blocking behavior, it is necessary to use a separate thread outside the event loop.

This is exactly why the [[Node.js]] core team created a native library called **libuv**, with the objective to make Node.js compatible with all the major operating systems and normalize the non- blocking behavior of the different types of resource. **`Libuv`** represents the **low-level** I/O engine of Node.js and is probably the most important component that Node.js is built on.

`libuv` also **implements** the [[Reactor pattern]], thus providing an API for creating event loops, managing the event queue, running asynchronous I/O operations, and queuing other types of task.

A great resource to learn more about libuv is the free online book created by [[Nikhil Marathe]], which is available at nodejsdp.link/uvbook.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[NodeJS Design Patterns]]
- Related links: [An introduction to libuv](nodejsdp.link/uvbook)