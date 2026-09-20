# 📱 React Native - Hard Questions From Notes

> **Topics from Notes Covered:** Streams, File System (`fs`), and Threading in React Native vs Node.js.

---

### Q1: Streams, `fs`, and Threads in React Native vs Node.js
**Question (From Notes):** Compare Streams, File System (`fs`), and Threads between React Native and Node.js.

**Answer:**
| Domain | Node.js | React Native |
| :--- | :--- | :--- |
| **File System (`fs`)** | Built-in `fs` and `fs/promises` core modules reading directly from OS disk. | No native core `fs`. Requires native community modules (`react-native-fs`, `expo-file-system`) crossing the native bridge/JSI. |
| **Streams** | Native `stream` module (`Readable`, `Writable`, `Transform`, `pipeline`) with backpressure control. | Streams must be bridged to native platform streams (iOS `NSInputStream`, Android `InputStream`) to prevent blocking the JS thread. |
| **Threading Model** | Main JS Thread + Libuv Thread Pool (4 threads for I/O) + `worker_threads`. | **3 Core Threads**:<br>1. **JS Thread**: Runs React component code.<br>2. **UI Main Thread**: Manages native views and gestures.<br>3. **Shadow Thread**: Computes Flexbox layout with Yoga engine. |

```
   Node.js Architecture:
   [JS Engine] <---> [Libuv Event Loop] <---> [Thread Pool / OS Kernel]

   React Native Architecture:
   [JS Thread] <=== JSI / Bridge ===> [Shadow Thread (Yoga)] <===> [UI Main Thread]
```
