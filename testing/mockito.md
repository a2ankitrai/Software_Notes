Mockito
---

# Mock vs. Spy in Mockito
 
When Mockito creates a mock – it does so from the Class of an Type, not from an actual instance. The mock simply creates a bare-bones shell instance of the Class, entirely instrumented to track interactions with it.

On the other hand, the spy will wrap an existing instance. It will still behave in the same way as the normal instance – the only difference is that it will also be instrumented to track all the interactions with it.

In the following example – we create a mock of the ArrayList class:

```
@Test
public void whenCreateMock_thenCreated() {
    List mockedList = Mockito.mock(ArrayList.class);
 
    mockedList.add("one");
    Mockito.verify(mockedList).add("one");
 
    assertEquals(0, mockedList.size());
}
```

As you can see – adding an element into the mocked list doesn’t actually add anything – it just calls the method with no other side-effect.

A spy on the other hand will behave differently – it will actually call the real implementation of the add method and add the element to the underlying list:

```
@Test
public void whenCreateSpy_thenCreate() {
    List spyList = Mockito.spy(new ArrayList());
 
    spyList.add("one");
    Mockito.verify(spyList).add("one");
 
    assertEquals(1, spyList.size());
}
```
 
In a mock all methods are stubbed and return "smart return types". This means that calling any method on a mocked class will do nothing unless you specify behaviour.

In a spy the original functionality of the class is still there but you can validate method invocations in a spy and also override method behaviour.

---


# PowerMockito 

PowerMockito is a PowerMock’s extension API to support Mockito. It provides capabilities to work with the Java Reflection API in a simple way to overcome the problems of Mockito, such as the lack of ability to mock final, static or private methods.

