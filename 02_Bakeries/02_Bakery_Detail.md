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

5. So we can map over them and return a list of cookie items! Let's do that!

```javascript
const cookieList = bakery.cookies.map((cookie) => (
  <CookieItem cookie={cookie} />
));
```

6. Let's call it and fix the styling a bit

```jsx
<div>
  <DetailWrapper>
    <h4>{bakery.name}</h4>
    <img src={bakery.image} />
  </DetailWrapper>
  <ListWrapper>{cookieList}</ListWrapper>
</div>
```
