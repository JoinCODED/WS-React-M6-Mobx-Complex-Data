Let's try deleting a cookie, we got an error!

1. Let's console log `bakery.cookies` in `BakeryDetail`. You'll see that now when we delete a cookie, it's replaced with an `undefined` which is throwing an error!

2. So basically we will filter our `cookies` and only return a `cookie` if it exists.

   ```javascript
   const cookies = bakery.cookies
     .map((cookie) => cookieStore.getCookieById(cookie.id))
     .filter((cookie) => cookie);
   ```

How cute is this?
