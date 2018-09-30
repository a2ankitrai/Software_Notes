HttpClient
---


## Reading the full response

The response body doesn't return all the data you may need. Sometimes servers return special headers or status codes to indicate certain conditions that are important to the application workflow.

Tell HttpClient that you want the full response with the observe option:

```ts
getConfigResponse(): Observable<HttpResponse<Config>> {
  return this.http.get<Config>(
    this.configUrl, { observe: 'response' });
}
```

Now `HttpClient.get()` returns an `Observable` of typed `HttpResponse` rather than just the `JSON` data.

```ts
showConfigResponse() {
  this.configService.getConfigResponse()
    // resp is of type `HttpResponse<Config>`
    .subscribe(resp => {
      // display its headers
      const keys = resp.headers.keys();
      this.headers = keys.map(key =>
        `${key}: ${resp.headers.get(key)}`);

      // access the body directly, which is typed as `Config`.
      this.config = { ... resp.body };
    });
}
```

---

## Error handling

### Getting error details

Two types of errors can occur. The server backend might reject the request, returning an HTTP response with a status code such as 404 or 500. These are error responses.

Or something could go wrong on the client-side such as a network error that prevents the request from completing successfully or an exception thrown in an RxJS operator. These errors produce JavaScript `ErrorEvent` objects.

The HttpClient captures both kinds of errors in its HttpErrorResponse and you can inspect that response to figure out what really happened.

```ts
private handleError(error: HttpErrorResponse) {
  if (error.error instanceof ErrorEvent) {
    // A client-side or network error occurred. Handle it accordingly.
    console.error('An error occurred:', error.error.message);
  } else {
    // The backend returned an unsuccessful response code.
    // The response body may contain clues as to what went wrong,
    console.error(
      `Backend returned code ${error.status}, ` +
      `body was: ${error.error}`);
  }
  // return an observable with a user-facing error message
  return throwError(
    'Something bad happened; please try again later.');
};
```

Now you take the Observables returned by the HttpClient methods and pipe them through to the error handler.

```ts
getConfig() {
  return this.http.get<Config>(this.configUrl)
    .pipe(
      catchError(this.handleError)
    );
}
```

---

## `retry()`

The RxJS library offers several retry operators that are worth exploring. The simplest is called `retry()` and it automatically re-subscribes to a failed Observable a specified number of times. Re-subscribing to the result of an `HttpClient` method call has the effect of reissuing the HTTP request.

Pipe it onto the `HttpClient` method result just before the error handler.

```ts
getConfig() {
  return this.http.get<Config>(this.configUrl)
    .pipe(
      retry(3), // retry a failed request up to 3 times
      catchError(this.handleError) // then handle the error
    );
}
```

---

## Requesting non-JSON data

By default `HttpClient` returns json data. Provide second arguement `{responseType: 'text'}` to the request to retrieve data with other type.

```ts
getTextFile(filename: string) {
  // The Observable returned by get() is of type Observable<string>
  // because a text response was specified.
  // There's no need to pass a <string> type parameter to get().
  return this.http.get(filename, {responseType: 'text'})
    .pipe(
      tap( // Log the result or error
        data => this.log(filename, data),
        error => this.logError(filename, error)
      )
    );
}
```

`HttpClient.get()` returns a string rather than the default JSON because of the `responseType` option.

---

## Sending data to the server

### Adding headers

create a header object

```ts
const httpOptions = {
  headers: new HttpHeaders({
    'Content-Type':  'application/json',
    'Authorization': 'my-auth-token'
  })
};
```

### Making a POST request

```ts
addHero (hero: Hero): Observable<Hero> {
  return this.http.post<Hero>(this.heroesUrl, hero, httpOptions)
    .pipe(
      catchError(this.handleError('addHero', hero))
    );
}
```

The `HttpClient.post()` method is similar to `get()` in that it has a type parameter (you're expecting the server to return the new hero) and it takes a resource URL.

It takes two more parameters:

- the data to POST in the body of the request.
- `httpOptions` - the method options which, in this case, specify required headers.


----

### Making a DELETE request

The `HttpClient.delete` method is used for the same.

```ts
deleteHero (id: number): Observable<{}> {
  const url = `${this.heroesUrl}/${id}`; // DELETE api/heroes/42
  return this.http.delete(url, httpOptions)
    .pipe(
      catchError(this.handleError('deleteHero'))
    );
}
```

Even though you may not be using the result, you still have to subscribe. Calling the subscribe() method executes the observable, which is what initiates the DELETE request.

In component

```ts
this.heroesService.deleteHero(hero.id).subscribe();
```

>You must call `subscribe()` or nothing happens. Just calling `Service.deleteHero()` **does not initiate the DELETE request**.

**Always subscribe!**

An `HttpClient` method does not begin its HTTP request until you call `subscribe()` on the observable returned by that method. This is true for all `HttpClient` methods.

> The `AsyncPipe` subscribes (and unsubscribes) for you automatically.

---

## Advanced usage

**Configuring the request** - Other aspects of an outgoing request can be configured via the options object passed as the last argument to the HttpClient method.

## Update headers

You can't directly modify the existing headers within the previous options object because instances of the `HttpHeaders` class are immutable.

Use the `set()` method instead. It returns a clone of the current instance with the new changes applied.

example for updating the authorization header (after the old token expired) before making the next request.

```ts
httpOptions.headers =
  httpOptions.headers.set('Authorization', 'my-new-auth-token');
```

## URL Parameters

```ts
/* GET heroes whose name contains search term */
searchHeroes(term: string): Observable<Hero[]> {
  term = term.trim();

  // Add safe, URL encoded search parameter if there is a search term
  const options = term ?
   { params: new HttpParams().set('name', term) } : {};

  return this.http.get<Hero[]>(this.heroesUrl, options)
    .pipe(
      catchError(this.handleError<Hero[]>('searchHeroes', []))
    );
}
```

The `HttpParams` are immutable so you'll have to use the set() method to update the options.














---
