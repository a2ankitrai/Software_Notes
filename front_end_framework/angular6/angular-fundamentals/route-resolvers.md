# Route Resolvers
---

One way to deal with getting and displaying data from an API is to route a user to a component, and then in that component’s `ngOnInit` hook call a method in a service to get the necessary data. While getting the data, perhaps the component can show a loading indicator. There’s another way however using what’s known as a route resolver, which allows you to get data before navigating to the new route.

## syntax of route resolver in route configuration

```
{
    path: 'edit-note/:id', component: NotesEditComponent, resolve: {
      note: NotesResolverService
    }

    ```


## References

- https://alligator.io/angular/route-resolvers/
