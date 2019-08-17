# Understanding RxJava Subject — Publish, Replay, Behavior and Async Subject

## What is Subject?

A Subject is a sort of bridge or proxy that is available in some implementations of ReactiveX that acts both as an observer and as an Observable. Because it is an observer, it can subscribe to one or more Observables, and because it is an Observable, it can pass through the items it observes by re-emitting them, and it can also emit new items.

There are four types of Subject available in RxJava.

- Publish Subject - It emits all the subsequent items of the source Observable at the time of subscription.

- Replay Subject - It emits all the items of the source Observable, regardless of when the subscriber subscribes

- Behavior Subject - It emits the most recently emitted item and all the subsequent items of the source Observable when an observer subscribes to it.


- Async Subject - It only emits the last value of the source Observable(and only the last value).

---

## Backpressure

In cases where a publisher is emitting items more rapidly than an operator or subscriber can consume them, then the items that are overflowing from the publisher need to be handled. If for example we try to maintain an ever-expanding buffer of items emitted by the faster publisher to eventually combine with items emitted by the slower one. This could result in OutOfMemoryError.

> Backpressure relates to a feedback mechanism through which the subscriber can signal to the producer how much data it can consume and so to produce only that amount
