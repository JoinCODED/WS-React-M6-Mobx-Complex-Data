But if you add a cookie, it's not added directly in `BakeryDetail`. It's only added in `CookieList`. That's because we need to add the new cookie's ID to the list of `cookies` in our `bakery`.

To do that, we will pass the `bakery` as an argument to `createCookie` in our `CookieModal`. But, how can we have access to it? Instead of passing `bakeryId` as a `prop` from `BakeryDetail` we will pass `bakery`.

1. In `BakeryDetail` pass `bakery.id` as a `prop` to `AddButton`.

   ```javascript
   <div className="col-12">
     <CookieList cookies={cookies} />
     <AddButton bakery={bakery} />
   </div>
   ```

2. In `AddButton`, replace every `bakeryId` with `bakery`.

3. In `CookieModal`, replace `bakery` with `bakeryId`, and remove `bakeryId` from your state.

   ```javascript
   const CookieModal = ({ bakery, isOpen, closeModal, oldCookie }) => {
   const [cookie, setCookie] = useState(
   oldCookie ?? {
     name: "",
     price: 0,
     description: "",
     image: "",
   }
   );
   ```

4. Pass `bakery` as a second argument to `createCookie`. Don't worry about `updateCookie`, since it needs one argument only it will ignore the second one.

   ```javascript
   const handleSubmit = (event) => {
     event.preventDefault();
     cookieStore[oldCookie ? "updateCookie" : "createCookie"](cookie, bakery);
     closeModal();
   };
   ```

5. In `cookieStore`, give `createCookie` another argument which is `bakery`.

   ```javascript
    createCookie = async (newCookie, bakery) => { [...] }
   ```

6. Change the request so that it takes the ID from `bakery.id`.

   ```javascript
   const res = await axios.post(
     `http://localhost:8000/bakeries/${bakery.id}/cookies`,
     formData
   );
   ```

7. Now, we will add the new cookie's ID to our `bakery`. First we have to check the syntax of the cookies in `bakery`.

8. So every cookie is represented in object with a property called `id`.

   ```javascript
   this.cookies.push(res.data);
   bakery.cookies.push({ id: res.data.id });
   ```

9. Try adding a cookie now. It works!
