What will we have in our bakery detail? The bakery's name and image, and a list of all its products.

1.  Let's start by defining a `BakeryDetail` component.

    ```javascript
    import React from "react";

    const BakeryDetail = () => {
      return <div>Bakery Detail</div>;
    };

    export default BakeryDetail;
    ```

2.  In `App.js`, let's create a route for `BakeryDetail`. Make sure to place it above `BakeryList`'s route:

    ```javascript
    <Route path="/bakeries/:bakerySlug">
      <BakeryDetail />
    </Route>
    ```

3.  Now, in `BakeryDetail`, `find` the `bakery` that has a `slug` equal to `bakerySlug`. We used the same `DetailWrapper` used in `CookieDetail`.

    ```javascript
    const BakeryDetail = () => {
      const { bakerySlug } = useParams();
      const bakery = bakeryStore.bakeries.find(
        (_bakery) => _bakery.slug === bakerySlug
      );
      return (
        <DetailWrapper>
          <h4>{bakery.name}</h4>
          <img src={bakery.image} />
        </DetailWrapper>
      );
    };
    ```

4.  Next, we want to render the list this bakery's `cookies`. If you console log `cookie`, you'll see that every `bakery` has a `cookies` list.

```javascript
console.log("BakeryDetail -> bakery", bakery);
```

So why not use the `CookieList` component instead of rewriting code?

5. Change `CookieList` so that it receives `cookies` as a `prop`.

   ```javascript
   const CookieList = ({ cookies }) => {
   const [query, setQuery] = useState("");

   const cookieList = cookies
   .filter((cookie) => cookie.name.toLowerCase().includes(query.toLowerCase()))
   .map((cookie) => <CookieItem cookie={cookie} key={cookie.id} />);
   ```

6. Pass `cookieStore.cookies` as a `prop` to `CookieList` in `Routes.js`. Don't forget to import `cookieStore`.

```jsx
<Route path="/cookies">
  <CookieList cookies={cookieStore.cookies} />
</Route>
```

7. In `BakeryDetail`, render `Cookieist` and pass `bakery.cookies` as a `prop`.

```jsx
<DetailWrapper>
  <h4>{bakery.name}</h4>
  <img src={bakery.image} />
  <UpdateButton bakery={bakery} />
</DetailWrapper>
<CookieList cookies={bakery.cookies} />
```

8. Let's fix the styling a bit in `BakeryDetail`.

```jsx
return (
  <div className="row">
    <div className="container">
      <DetailWrapper className="col-12">
        <h4>{bakery.name}</h4>
        <img src={bakery.image} />
        <UpdateButton bakery={bakery} />
      </DetailWrapper>
    </div>
    <div className="col-12">
      <CookieList cookies={bakery.cookies} />
    </div>
  </div>
);
```

Amazing! Look at that! We even have a search bar and an add button!
