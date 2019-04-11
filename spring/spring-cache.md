# Spring Cache

Caching is a way to store frequently needed information so that it’s readily available when needed.

Although Spring doesn’t implement a cache solution, it offers declarative support for caching that integrates with several popular caching implementations.

---

Under the covers, `@EnableCaching` and `<cache:annotation-driven>` work the same way. They create an aspect with pointcuts that trigger off of Spring’s caching annotations.

Cache managers are the heart of Spring’s cache abstraction, enabling integration with one of several popular caching implementations.

CompositeCacheManager is configured with one or more cache managers and iterates over them all as it tries to find a previously cached value.

the `@Cacheable` and `@CachePut` annotations can both populate a cache. They work in slightly different ways, though.

`@Cacheable` looks for an entry in the cache first, preempting the method invocation if a matching entry is found. If no matching
entry is found, the method is invoked and the value returned is put in the cache.

`@CachePut`, on the other hand, never checks for a matching value in the cache, always allows the target method to be invoked, and adds the returned value to the cache.

---

## Unless and condition attribute

On the surface, it may seem that unless and condition accomplish the same thing. There’s a subtle difference, though. The unless attribute can only prevent an object from being placed in the cache. But the cache is still searched when the method is called, and if a match is found, it’s returned. On the other hand, if condition’s expression evaluates to false, then caching is disabled for the duration of the method invocation. The cache isn’t searched, nor is the return value placed in the cache.

Under what circumstances might you want to remove something from the cache? Any time a cached value is no longer valid, you should make sure it’s removed from the cache so that future cache hits won’t return stale or otherwise nonexistent data.

## CacheEvict

if an `@CacheEvict`-annotated method is called, one or more entries are removed from the cache.

Unlike `@Cacheable` and `@CachePut`, `@CacheEvict` can be used on void methods. `@Cacheable` and `@CachePut` require a non-void return value, which is the item to place in the cache.


## Cache Abstraction

### Cache vs Buffer

The terms "buffer" and "cache" tend to be used interchangeably; note however they represent different things. A buffer is used traditionally as an intermediate temporary store for data between a fast and a slow entity. As one party would have to wait for the other affecting performance, the buffer alleviates this by allowing entire blocks of data to move at once rather then in small chunks. The data is written and read only once from the buffer. Furthermore, the buffers are visible to at least one party which is aware of it.

A cache on the other hand by definition is hidden and neither party is aware that caching occurs.It as well improves performance but does that by allowing the same data to be read multiple times in a fast fashion.

---

Just like other services in the Spring Framework, the caching service is an abstraction (not a cache implementation) and requires the use of an actual storage to store the cache data - that is, the abstraction frees the developer from having to write the caching logic but does not provide the actual stores. This abstraction is materialized by the `org.springframework.cache.Cache` and `org.springframework.cache.CacheManager` interfaces.

Caching a particular item is a direct equivalent of the typical get-if-not-found-then- proceed-and-put-eventually code blocks found with programmatic cache interaction: no locks are applied and several threads may try to load the same item concurrently. The same applies to eviction: if several threads are trying to update or evict data concurrently, you may use stale data.


To use the cache abstraction, the developer needs to take care of two aspects:

- **caching declaration** - identify the methods that need to be cached and their policy

- **cache configuration** - the backing cache where the data is stored and read from

---

































---
