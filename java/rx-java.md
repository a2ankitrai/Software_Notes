Rx Java
---

## The Basics

In reactive programming the consumer reacts to the data as it comes in. This is the reason why asynchronous programming is also called reactive programming. Reactive programming allows to propagates event changes to registered observers.

RxJava is the Java implementation of this concept. RxJava is published under the Apache 2.0 license. RxJava provides Java API for asynchronous programming with observable streams.

Reactive programming provides a simple way of asynchronous programming. This allows to simplify the asynchronously processing of potential long running operations. It also provides a defined way of handling multiple events, errors and termination of the event stream. Reactive programming provides also a simplified way of running different tasks in different threads.

## Build blocks for RxJava
 

- `observables` representing sources of data

- `subscribers` (or observers) listening to the observables

- a set of methods for modifying and composing the data

An observable emits items; a subscriber consumes those items.

### Observables

Observables are the sources for the data. Usually they start providing data once a subscriber starts listening. An observable may emit any number of items (including zero items). It can terminate either successfully or with an error. Sources may never terminate, for example, an observable for a button click can potentially produce an infinite stream of events.


### Subscribers

A observable can have any number of subscribers. If a new item is emitted from the observable, the `onNext()` method is called on each subscriber. If the observable finishes its data flow successful, the `onComplete()` method is called on each subscriber. Similar, if the observable finishes its data flow with an error, the `onError()` method is called on each subscriber.

---


## Creating Observables, subscribing to them and disposing them

### Creating observables

![observable_types](./images/observable_types.png)

An example for the usage of `Flowable`, is when you process touch events. You cannot control the user who is doing these touch events, but you can tell the source to emit the events on a slower rate in case you cannot processes them at the rate the user produces them.


### Convenience methods to create observables**

RxJava provides several convenience methods to create observables

- `Observable.just("Hello")` - Allows to create an observable as wrapper around other data types

- `Observable.fromIterable()` - takes an `java.lang.Iterable<T>` and emits their values in their order in the data structure

- `Observable.fromArray()` - takes an array and emits their values in their order in the data structure

- `Observable.fromCallable()` - Allows to create an observable for a `java.util.concurrent.Callable<V>`

- `Observable.fromFuture()` - Allows to create an observable for a `java.util.concurrent.Future`

- `Observable.interval()` - An observable that emits Long objects in a given interval


Similar methods exists for the other data types, e.g., `*Flowable.just()`, `Maybe.just()` and `Single.just`.


### Subscribing in RxJava

To receive the data emitted from an observable you need to subscribe to it. observables offer a large variety of subscribe methods.

```java

Observable<Todo> todoObservable = Observable.create(emitter -> { ... });

// Simply subscribe with a io.reactivex.functions.Consumer<T>, which will be informed onNext()
Disposable disposable = todoObservable.subscribe(t -> System.out.print(t));

// Dispose the subscription when not interested in the emitted data any more
disposable.dispose();

// Also handle the error case with a second io.reactivex.functions.Consumer<T>
Disposable subscribe = todoObservable.subscribe(t -> System.out.print(t), e -> e.printStackTrace());
```

### Disposing subscriptions and using CompositeDisposable

When listers or subscribers are attached they usually are not supposed to listen eternally.

So it could happen that due to some state change the event being emitted by an observable might be not interesting any more.

```java

import io.reactivex.Single;
import io.reactivex.disposables.Disposable;
import io.reactivex.observers.DisposableSingleObserver;

Single<List<Todo>> todosSingle = getTodos();

Disposable disposable = todosSingle.subscribeWith(new DisposableSingleObserver<List<Todo>>() {

    @Override
    public void onSuccess(List<Todo> todos) {
        // work with the resulting todos
    }

    @Override
    public void onError(Throwable e) {
        // handle the error case
    }
});

// continue working and dispose when value of the Single is not interesting any more
disposable.dispose();

```


*The `Single` class and other observable classes offer different subscribe methods, which return a `Disposable` object.*


When working with multiple subscriptions, which may become obsolete due to the same state change using a `CompositeDisposable` is pretty handy to dispose a collection of subscriptions.

```java

import io.reactivex.Single;
import io.reactivex.disposables.CompositeDisposable;
import io.reactivex.observers.DisposableSingleObserver;

public class CompositeDisposableTest {

	public static void main(String[] args) {
		
		CompositeDisposable compositeDisposable = new CompositeDisposable();
		
		Single<String> single1 = Single.just("Alpha");
		Single<String> single2 = Single.just("Beta");
		Single<String> single3 = Single.just("Gamma");
		
		compositeDisposable.add(single1.subscribeWith(new DisposableSingleObserver<String>() {
		    @Override
		    public void onError(Throwable e) {
		        // handle the error case
		    }

			@Override
			public void onSuccess(String t) {
				System.out.println(t);
			}
		}));
		
		compositeDisposable.add(single2.subscribe(System.out::println));
		 
		compositeDisposable.add(single3.subscribe(System.out::println));
		
		compositeDisposable.dispose();
	}
}
```


---

## Caching values of completed observables

When working with observables doing async calls on every subscription on an observable is often not necessary.

It likely happens that observables are passed around in the application, without the need to do an such an expensive call all the time a subscription is added.

The below code snippet makes use of the `cache` method, so that the `Single` instance keeps its result, once it was successful for the first time.

```java

Single<List<Todo>> todosSingle = Single.create(emitter -> {
    Thread thread = new Thread(() -> {
        try {
            List<Todo> todosFromWeb = // query a webservice

            System.out.println("I am only called once!");

            emitter.onSuccess(todosFromWeb);
        } catch (Exception e) {
            emitter.onError(e);
        }
    });
    thread.start();
});

// cache the result of the single, so that the web query is only done once
Single<List<Todo>> cachedSingle = todosSingle.cache();

cachedSingle.subscribe(... " Show todos times in a bar chart " ...);

showTodosInATable(cachedSingle);

cachedSingle.subscribe(... " Show todos in gant diagram " ...);

anotherMethodThatsSupposedToSubscribeTheSameSingle(cachedSingle);

```

[Github Repo Link](https://github.com/a2ankitrai/Rx-Java-Test)


 
