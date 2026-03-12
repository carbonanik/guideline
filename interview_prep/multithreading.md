# Multithreading & Asynchronous Programming

## Single-Threaded Nature of Dart
Dart runs in a single thread of execution called an **Isolate**. It uses an **Event Loop** to handle asynchronous tasks.

### Isolate
- An Isolate is a private space of memory and a single thread running an event loop.
- **No Shared Memory:** Isolates don't share memory. Communication happens only via **Messages** (ports).
- **Dart Memory Model:** Every isolate has its own heap. Garbage collection happens independently per isolate, which prevents "stop-the-world" pauses for the entire app.
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
- `Isolate.spawn`: More low-level, allows persistent communication between isolates using `SendPort` and `ReceivePort`.

## 4. Future: No Await (Fire-and-Forget)
Calling a future without `await` starts its execution asynchronously but continues the current function immediately.
- **Risk:** Unhandled exceptions (if the future fails, the app might crash if no `.catchError` is provided).
- **Pattern:** Use `unawaited(future)` from `dart:async` to explicitly mark that you don't care about the result.

## 5. Comparison: Future vs. Stream vs. Isolate

| Feature | Future | Stream | Isolate |
| --- | --- | --- | --- |
| **Result** | Single result | Multiple events | Independent task |
| **Thread** | Same (UI) | Same (UI) | New (Worker) |
| **Use Case** | API Call | Websockets, Taps | Heavy Image Processing |

## Summary Table

| Concept | Description |
| --- | --- |
| **Async/Await** | Concurrency without multithreading (waiting for I/O). |
| **Isolates** | True parallelism (running calculations on separate CPU cores). |
| **Event Loop** | The mechanism that coordinates execution. |

## Dart Language Features (Senior Level)

### 1. Sound Null Safety
Dart’s null safety is "Sound," meaning if the type system says a variable isn't null, it can *never* be null at runtime.
- **`?`**: Nullable type.
- **`!`**: Assertion operator (use only when 100% sure).
- **`late`**: Lazily initialized. Helpful for variables initialized in `initState`.
- **`required`**: Named parameters that must be provided.

### 2. Dart Patterns & Records (Dart 3+)
- **Records**: Allow returning multiple values from a function without a custom class.
  - `(double, double) getLocation() => (10.0, 20.0);`
- **Pattern Matching**: Switch expressions and destructuring.
  - `switch (response) { case Success(:var data) => ... }`

### 3. Streams & RxDart
- **StreamController**: Manages a stream's lifecycle.
- **Broadcast Stream**: Allows multiple listeners (default streams only allow one).
- **RxDart**: Adds powerful operators like `debounceTime`, `switchMap`, and `combineLatest`. Essential for complex search or form validation logic.

---
**Next Sitting Recommendation:** [State Management](./state_management.md) to learn how to manage shared data in Flutter.
