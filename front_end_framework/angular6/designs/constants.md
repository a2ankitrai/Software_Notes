Creating constants
---

Create a constant typescript class

```ts
export class AppConstants {
   public static get baseURL(): string { return "http://localhost:9000"; }
}
```

You can use the same now as follows:

```ts
import{ AppConstants} from '../app/constants'

...
...


this._baseURL = AppConstants.baseURL;
 ```
