For the data to be coming from one place only, we will fix the backend so that it sends a list of IDs only.

1. In `cookieStore`, we will create a method called `getCookieById` that takes a `cookieId` as an argument and returns the found cookie.

   ```javascript
   getCookieById = (cookieId) =>
     this.cookies.find((cookie) => cookie.id === cookieId);
   ```

Now in `bakeryDetail`, we can't pass `bakery.cookies` directly to `CookieList`, because it's a list of IDs only. So what can we do?

2. We will `map` over the IDs in `bakery.cookies` and return the `cookie` from `cookieStore` using the method `getCookieById`.

   ```javascript
   const cookies = bakery.cookies.map((cookie) =>
     cookieStore.getCookieById(cookie.id)
   );
   ```

3. Now, we will pass `cookies` to `CookieList` instead of passing `bakery.cookies`.

   ```javascript
   <CookieList cookies={cookies} />
   ```
