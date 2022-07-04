
**JavaScript is an interpreted language, not a compiled one. This means that it needs an interpreter which converts the JS code to a machine code. There are several types of interpreters (known as engines). The most popular browser engines are V8 (Chrome), Quantum (Firefox) and WebKit (Safari). Incidentally, V8 is also used in a popular non-browser runtime, Node.js.

Each engine contains a memory heap, a call stack, an event loop, a callback queue and a WebAPI with HTTP requests, timers, events, etc., all implemented in its own way for faster and safer interpretation of the JS code.**




![](https://thecodest.co/images/uploaded/2020/03/asynchronous-and-single-threaded-javascript-meet-the-event-loop/runtime-architecture.png)


## **Single Thread**

A single-thread language is one with a single call stack and a single memory heap. It means that it runs only one thing at a time.

A `stack` is a continuous region of memory, allocating local context for each executed function.

A `heap` is a much larger region, storing everything allocated dynamically.

A `call stack` is a data structure which basically records where we are in the program.


![](https://thecodest.co/images/uploaded/2020/03/asynchronous-and-single-threaded-javascript-meet-the-event-loop/stack.gif)

As you can see, the functions are added to the stack, executed and later deleted. It's the so-called LIFO way - Last In, First Out. Each entry in the call stack is called a `stack frame`.

Knowledge of the call stack is useful for reading error stack traces. Generally, the exact reason for the error is at the top in first line, though the order of code execution is bottom-up.

Sometimes you can deal with a popular error, notified by `Maximum call stack size exceeded`. It is easy to get this using recursion:

```
function foo() {
    foo()
}
foo()
```




### **Concurrency & Parallelism**

`Concurrency` means executing multiple tasks at the same time but not simultaneously. E.g. two tasks works in overlapping time periods.

`Parallelism` means performing two or more tasks simultaneously, e.g. performing multiple calculations at the same time.

### [](https://thecodest.co/blog/asynchronous-and-single-threaded-javascript-meet-the-event-loop/#threads--processes)**Threads & Processes**

`Threads` are a sequence of code execution which can be executed independently of one another.

`Process` is an instance of a running program. A program can have multiple processes.

### [](https://thecodest.co/blog/asynchronous-and-single-threaded-javascript-meet-the-event-loop/#synchronous--asynchronous)**Synchronous & Asynchronous**

In `synchronous` programming, tasks are executed one after another. Each task waits for any previous task to be completed and is executed only then.

In `asynchronous` programming, when one task is executed, you can switch to a different task without waiting for the previous one to be completed.

### [](https://thecodest.co/blog/asynchronous-and-single-threaded-javascript-meet-the-event-loop/#synchronous-and-asynchronous-in-a-single-and-multi-threaded-environment)**Synchronous and Asynchronous in a Single and Multi-threaded Environment**

`Synchronous with a single thread`: Tasks are executed one after another. Each task waits for its previous task to get executed.

`Synchronous with multiple threads`: Tasks are executed in different threads but wait for any other executing tasks on any other thread.

`Asynchronous with a single thread`: Tasks start being executed without waiting for a different task to finish. At a given time, only a single task can be executed.

`Asynchronous with multiple threads`: Tasks get executed in different threads without waiting for other tasks to be completed and finish their executions independently.



Asynchronous: Go away and do this task, when you're finished come back and tell me and bring the results. I'll be getting on with other things in the mean time.

Parallel: I want you to do this task. If it makes it easier, get some folks in to help. This is urgent though, so I'll wait here until you come back with the results. I can do nothing else until you come back.


When you run something asynchronously it means it is non-blocking, you execute it without waiting for it to complete and carry on with other things. Parallelism means to run multiple things at the same time, in parallel. Parallelism works well when you can separate tasks into independent pieces of work.





**asynchronous calls** will use **threads already in use by the system** and **parallel programming** requires **the developer to break the work up, spinup, and teardown threads needed**.


**Async** and **Callbacks** are generally a way (tool or mechanism) to express concurrency i.e. a set of entities possibly talking to each other and sharing resources. In the case of async or callback communication is implicit while sharing of resources is optional (consider RMI where results are computed in a remote machine). As correctly noted this is usually done with responsiveness in mind; to not wait for long **latency** events.

Parallel programming has usually throughput as the main objective while latency, i.e. the completion time for a single element, might be worse than a equivalent sequential program.

To better understand the distinction between concurrency and parallelism I am going to quote from _Probabilistic models for concurrency_ of Daniele Varacca which is a good set of notes for theory of concurrency:

> A model of computation is a model for concurrency when it is able to represent systems as composed of independent autonomous components, possibly communicating with each other. **The notion of concurrency should not be confused with the notion of parallelism. Parallel computations usually involve a central control which distributes the work among several processors. In concurrency we stress the independence of the components, and the fact that they communicate with each other.** Parallelism is like ancient Egypt, where the Pharaoh decides and the slaves work. Concurrency is like modern Italy, where everybody does what they want, and all use mobile phones.

**In conclusion**, parallel programming is somewhat a special case of concurrency where separate entities collaborate to obtain high performance and throughput (generally).

Async and Callbacks are just a mechanism that allows the programmer to express concurrency. Consider that well-known parallel programming design patterns such as master/worker or map/reduce are implemented by frameworks that use such lower level mechanisms (async) to implement more complex **centralized** interactions.

ref:
- https://stackoverflow.com/questions/6133574/how-to-articulate-the-difference-between-asynchronous-and-parallel-programming#:~:text=When%20you%20run%20something%20asynchronously,into%20independent%20pieces%20of%20work.
- https://urda.com/blog/2010/10/04/asynchronous-versus-parallel-programming