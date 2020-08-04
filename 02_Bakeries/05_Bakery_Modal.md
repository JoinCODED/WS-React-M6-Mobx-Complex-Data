1. Create a `BakeryModal` component. The easiest way is to copy the `CookieModal` and fix the fields. Keep in mind that every bakery need two fields, `name` and `image` only.

2. Now, how can we call it? In your `AddButton`, we will add a condition that whenever the button is clicked it will either open the `CookieModal` or `BakeryModal`.

3. The difference between the two is that the `CookieModal` needs `bakeryId`, so if a `bakeryId` exists we will render `CookieModal`, else we will render `BakeryModal`.

   ```javascript
   {
     bakeryId ? (
       <CookieModal
         bakeryId={bakeryId}
         isOpen={isOpen}
         closeModal={closeModal}
       />
     ) : (
       <BakeryModal isOpen={isOpen} closeModal={closeModal} />
     );
   }
   ```

4. Let's try creating a new bakery. Yes! It works!

After creating a bakery, if you visit it directly you'll get an error. That's because when a bakery is first created, it doesn't have a `cookies` field.

5. So in `CookieList`, we will give `cookies` a default value of an empty array.

   ```javascript
   const CookieList = ({ cookies = [] }) => {
   ```

Now it works perfectly.

Updating the bakery is very similar to creating one. But what will the condition be? Updating a cookie requires no bakery.

6. Let's start with rendering the `Update` button in `BakeryDetail` and passing it `bakery`.

   ```jsx
   <DetailWrapper className="col-12">
     <h4>{bakery.name}</h4>
     <img src={bakery.image} />
     <UpdateButton bakery={bakery} />
   </DetailWrapper>
   ```

7. In `UpdateButton`, we have one of two choices, check if `cookie` or `bakery` exists. I'll check for the `bakery`.

   ```jsx
   {
     bakery ? (
       <BakeryModal
         isOpen={isOpen}
         closeModal={closeModal}
         oldBakery={bakery}
       />
     ) : (
       <CookieModal
         isOpen={isOpen}
         closeModal={closeModal}
         oldCookie={cookie}
       />
     );
   }
   ```
