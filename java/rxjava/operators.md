# Operators

Operators are basically a set of functions that can operate on any observable and defines the observable, how and when it should emit the data stream.

Few useful operators are as follows:

- Map: It transforms the items emitted by an Observable by applying a function to each item.

- Zip: It combines the emissions of multiple Observables together via a specified function, then emits a single item for each combination based on the results of this function.

- Filter: It emits only those items from an Observable that pass a predicate test.

- FlatMap: It transforms the items emitted by an Observable into Observables, then flattens the emissions from those into a single Observable.

- Take: It emits only the first n items emitted by an Observable.

- Reduce: It applies a function to each item emitted by an Observable, sequentially, and emits the final value.

- Skip: It suppresses the first n items emitted by an Observable.

- Buffer: It periodically gathers items emitted by an Observable into bundles and emits these bundles rather than emitting the items one at a time.

- Concat: It emits the emissions from two or more Observables without interleaving them.

- Replay: It ensures that all observers see the same sequence of emitted items, even if they subscribe after the Observable has begun emitting items.

- Merge: It combines multiple Observables into one by merging their emissions.

---
