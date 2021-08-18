Async/Await allows you to have tasks that can yield their "turn" to another task if they are waiting for something to happen. Generally that is IO as mentioned in the other comment.

Those tasks can be scheduled by the asynchronous runtime on a single thread, or more. But parallelism is not a necessary element of it. You might have different tasks that are all in progress, but are not necessarily actively running at the same time, rather taking turns with some waiting in between.

Threads mean having multiple threads running at the same time, in parallel. Generally, that means something running at the same time as something else is running.

If you read a file in a thread(in a non asynchronous way) the thread is occupied until the file is read. If you read the file in an asynchronous manner, the thread can have other tasks scheduled on it while the file is being read.

Async/await and threads/atomics are not exclusive. In fact, asynchronous runtimes are often used with a threadpool that schedules those tasks onto multiple threads. So you can have the benefits of both quite easily. You will still need atomics to some extend(preferably ones optimized for async use) if you share data between tasks, unless they are shared only between tasks being scheduled on a single thread maybe.
