1. Create a `BakeryModal` component. The easiest way is to copy the `CookieModal` and fix the fields. Keep in mind that every bakery need two fields, `name` and `image` only.

2. Now, how can we call it? In your `AddButton`, we will add a condition that whenever the button is clicked it will either open the `CookieModal` or `BakeryModal`.

3. The difference between the two is that the `CookieModal` needs `bakeryId`, so if a `bakeryId` exists we will render `CookieModal`, else we will render `BakeryModal`.

```javascript
{
  bakeryId ? (
    <CookieModal bakeryId={bakeryId} isOpen={isOpen} closeModal={closeModal} />
  ) : (
    <BakeryModal isOpen={isOpen} closeModal={closeModal} />
  );
}
```

4. Let's try creating a new bakery. Yes! It works!
