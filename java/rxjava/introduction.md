# RxJava Introduction
---

**RxJava is a Java VM implementation of Reactive Extensions.**

From the official doc, Reactive Extensions(ReactiveX) is as a library for composing asynchronous and event-based programs by using observable sequences.

- Asynchronous: Different parts of the program run simultaneously.

- Event-Based: The program executes the code based on the event generated.

- The Reactive Extension is further elaborated: It extends the observer pattern to support sequences of data and/or events and adds operators that allow you to compose sequences together declaratively while abstracting away concerns about things like low-level threading, synchronization, thread-safety, concurrent data structures, and non-blocking I/O.

> Here, observer pattern is the key to understand the architecture, which is a software design pattern, where Subject maintains its Observers and notifies them automatically of any state change, usually by calling one of their methods.

---

There are two main components of RxJava:

- Observable: it emits the values.
- Observer: it gets the values.

Observer get the emitted values from Observable by subscribing on it.

All components are as follows:

- Flowable, Observable, Single, and Completable - does some work and emit values.
- Subscription - work is going on or completed or is used to cancel.
- Operators - Modify Data
- Schedulers - Where the work should be done, which thread like main thread, etc.
- Subscriber/Disposable - where the response will be sent after work has been completed.

---

## Types of Observables

Observables produce stream to be observed by an Observer when it subscribes. There are various types and ways this stream can be emitted and it depends on the use case. Some of those use cases are as listed below:

- Items are to be emitted one by one.
- Items are to be emitted by controlling the producers emission(with back pressure).
- Only one item need to be emitted as part of success.
- Item has to be emitted based on conditions.

There are 5 types of observables as follows:

- Observable: It emits 0..N elements, and then completes successfully or with an error.
- Flowable: Similar to Observable but with a backpressure strategy.
- Single: It completes with a value successfully or an error.(doesn’t have onComplete callback, instead onSuccess(val)).
- Maybe: It completes with/without a value or completes with an error.
- Completable: It just signals if it has completed successfully or with an error.

---

## Schedulers

RxJava Schedulers is all about managing thread at low level. They provide high-level constructs to manage with concurrency and deal with details by itself. They create workers who are responsible for scheduling and running code. By default RxJava will not introduce concurrency and will run the operations on the subscription thread.

There are two methods through which we can introduce Schedulers into our chain of operations:

- `subscribeOn`: It specify which Scheduler invokes the code contained in Observable.create().
- `observeOn`: It allows control to which Scheduler executes the code in the downstream operators.

RxJava provides some general use Schedulers:

- `Schedulers.computation()` : Used for CPU intensive tasks.
- `Schedulers.io()`: Used for IO bound tasks.
- `Schedulers.from(Executor)`: Use with custom ExecutorService.
- `Schedulers.newThread()`: It always creates a new thread when a worker is needed. Since it’s not thread pooled and always creates a new thread instead of reusing one, this scheduler is not very useful.
