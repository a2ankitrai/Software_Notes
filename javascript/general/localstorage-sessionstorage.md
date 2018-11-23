# localStorage and sessionStorage
---

`localStorage` and `sessionStorage`, part of the web storage API, are two great tools to save key/value pairs locally.

---

## localStorage vs sessionStorage

`localStorage` and `sessionStorage` accomplish the exact same thing and have the same API, but with `sessionStorage` the data is persisted only until the window or tab is closed, while with `localStorage` the data is persisted until the user manually clears the browser cache or until your web app clears the data.

---

## Creating Entries

Create key/value pair entries with `localStorage.setItem`, providing a key and a value:

```js
let key = 'Item 1';
localStorage.setItem(key, 'Value');
```
---

## Reading Entries

Read entries with `localStorage.getItem`:

```js
let myItem = localStorage.getItem(key);
```
---

## Updating Entries

Update an entry just as you would create a new one with setItem, but with a key that already exists:

```js
localStorage.setItem(key, 'New Value');
```

---

## Deleting Entries

Delete an entry with the removeItem method:

```js
localStorage.removeItem(key);
```

---

## Clearing Everything

Here’s how to clear everything that’s stored in `localStorage`:

```js
localStorage.clear();
```

---

## Storing Json Objects

Only strings can be stored with `localStorage` or `sessionStorage`, but you can use `JSON.stringify` to store more complex objects and JSON.parse to read them:

```js
// Create item:
let myObj = { name: 'Skip', breed: 'Labrador' };
localStorage.setItem(key, JSON.stringify(myObj));

// Read item:
let item = JSON.parse(localStorage.getItem(key));
```

---

## Checking for Items

Here’s how you can test for the presence of items in the `localStorage`:

```js
if (localStorage.length > 0) {
  // We have items
} else {
  // No items
}
```

---

## Checking for Support

Test for `localStorage` support by checking if it’s available on the window object:

```js
if (window.localStorage) {
  // localStorage supported
}
```

---

## Iterating Over Items

`localStorage` or `sessionStorage` don’t have a forEach method, but you can iterate over the items with a good old for loop:

```js
for (let i = 0; i < localStorage.length; i++){
  let key = localStorage.key(i);
  let value = localStorage.getItem(key);
  console.log(key, value);
}
```

---

# References

- https://alligator.io/js/introduction-localstorage-sessionstorage/
