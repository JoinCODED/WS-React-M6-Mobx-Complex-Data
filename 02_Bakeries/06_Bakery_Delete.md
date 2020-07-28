The same process goes for deleting a bakery.

1. Start with rendering the `DeleteButton` in `BakeryDetail` and pass it the bakery ID as a `prop`.

```jsx
<DeleteButton bakeryId={bakery.id} />
```

2. In `DeleteButton`, add a condition in `handleDelete`. If `bakeryId` is passed, call `bakeryStore.deleteBakery`.

```javascript
const handleDelete = () => {
  if (bakeryId) {
    bakeryStore.deleteBakery(bakeryId);
    history.push("/bakeries");
  } else {
    cookieStore.deleteCookie(cookieId);
    history.push("/cookies");
  }
};
```
