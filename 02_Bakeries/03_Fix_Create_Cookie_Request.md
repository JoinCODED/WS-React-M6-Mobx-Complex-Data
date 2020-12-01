We need to fix the create cookie method.

1. Let's start with fixing the request URL in the `createCookie` method in `cookieStore`.

But where will we get the ID from? Our `cookies` have no access to a bakery ID. We need to pass the bakery ID from `BakeryDetail` to `AddButton`, then to `CookieModal`.

2. In `BakeryDetail`, render the `AddButton` and pass it the ID as a `prop`.

   ```jsx
   <div className="col-12">
     <CookieList cookies={bakery.cookies} />
     <AddButton bakeryId={bakery.id} />
   </div>
   ```

3. In `AddButton`, pass `bakeryId` to `CookieModal`.

   ```jsx
   <CookieModal bakeryId={bakeryId} isOpen={isOpen} closeModal={closeModal} />
   ```

4. In `CookieModal`, pass the `bakeryId` to the `cookie` state.

   ```jsx
   {
     bakeryId: bakeryId,
     name: "",
     price: 0,
     description: "",
     image: "",
   }
   ```

5. NOW, in `createCookie` method in the `cookieStore`, pass the `bakeryId` in the URL, and let's test it out!

   ```javascript
   const res = await axios.post(
     `http://localhost:8000/bakeries/${newCookie.bakeryId}/cookies`,
     formData
   );
   ```

6. Yaaay! It's working! Keep in mind that we can only add a cookie from the bakery detail now.
