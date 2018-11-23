# RxJs
---

learning rx js to create better responsive mock in ns-angular client rather than developing things end to end.


---

Reactive programming is programming with asynchronous data streams.

On top of that, you are given an amazing toolbox of functions to combine, create and filter any of those streams. That's where the "functional" magic kicks in. A stream can be used as an input to another one. Even multiple streams can be used as inputs to another stream. You can merge two streams. You can filter a stream to get another one that has only those events you are interested in. You can map data values from one stream to another new one.

A stream is a sequence of **ongoing events ordered in time**. It can emit three different things: a value (of some type), an error, or a "completed" signal.

We capture these emitted events only asynchronously, by defining a function that will execute when a value is emitted, another function when an error is emitted, and another function when 'completed' is emitted. Sometimes these last two can be omitted and you can just focus on defining the function for values. The "listening" to the stream is called subscribing. The functions we are defining are observers. The stream is the subject (or "observable") being observed.

---

ReactiveX combines the Observer pattern with the Iterator pattern and functional programming with collections to fill the need for an ideal way of managing sequences of events.


The essential concepts in RxJS which solve async event management are:

- Observable: represents the idea of an invokable collection of future values or events.

- Observer: is a collection of callbacks that knows how to listen to values delivered by the Observable.

- Subscription: represents the execution of an Observable, is primarily useful for cancelling the execution.

- Operators: are pure functions that enable a functional programming style of dealing with collections with operations like map, filter, concat, flatMap, etc.

- Subject: is the equivalent to an EventEmitter, and the only way of multicasting a value or event to multiple Observers.

- Schedulers: are centralized dispatchers to control concurrency, allowing us to coordinate when computation happens on e.g. setTimeout or requestAnimationFrame or others.

































---
