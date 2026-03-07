# Multithreading & Asynchronous Programming

## Single-Threaded Nature of Dart
Dart runs in a single thread of execution called an **Isolate**. It uses an **Event Loop** to handle asynchronous tasks.

### Isolate
- An Isolate is a private space of memory and a single thread running an event loop.
- **No Shared Memory:** Isolates don't share memory. Communication happens only via **Messages** (ports).
- **Benefit:** No need for locks or shared state management, which prevents many common concurrency bugs.

## The Event Loop
The Event Loop continuously checks two queues:
1. **Microtask Queue:** High-priority internal tasks (rarely used by developers directly).
2. **Event Queue:** External events like I/O, timers, user taps, and futures.

> [!IMPORTANT]
> The Microtask queue is always processed completely before the next item in the Event Queue is handled.

## Asynchronous Tools

### 1. Future
Represents a value that will be available at some point in the future.
- `await`: Pauses the execution of the current function until the future completes.
- `.then()`: Registers a callback for when the future completes.

### 2. Stream
A sequence of asynchronous events. Think of it as a "pipe" where data flows over time.

## Heavy Computations
Since Dart is single-threaded, a long-running calculation will "block" the UI, causing jank.

### Solution: `Isolate.spawn` or `compute`
- `compute`: A high-level wrapper to run a function in a separate isolate and return the result. Best for one-off heavy tasks.
- `Isolate.spawn`: More low-level, allows persistent communication between isolates using `SendPort` and `ReceivePort`.

## Summary Table

| Concept | Description |
| --- | --- |
| **Async/Await** | Concurrency without multithreading (waiting for I/O). |
| **Isolates** | True parallelism (running calculations on separate CPU cores). |
| **Event Loop** | The mechanism that coordinates execution. |
