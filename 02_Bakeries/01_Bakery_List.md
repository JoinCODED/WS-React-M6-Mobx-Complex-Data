Let's start with creating a store for our bakeries and setting up our CRUD methods.

1. In the `stores` folder, create a file called `bakeryStore.js`.

2. The fastest way to setup our store is by copying our `cookieStore` and changing every cookie to bakery. But we only want the create and fetch methods. Easy right?

3. Let's create a bakery list component. Create a `BakeryList.js` for your file. We'll give it basic styling, a `container` class name and a title that already exist in our `styles` file.

   ```javascript
   // Styles
   import { Title } from "../../styles";

   const BakeryList = () => {
     return (
       <div className="container">
         <Title>Bakeries</Title>
       </div>
     );
   };

   export default BakeryList;
   ```

4. Then, let's create a route for our bakeries in `App.js`. Don't forget to import `BakeryList`.

   ```javascript
   <Route path="/bakeries">
     <BakeryList />
   </Route>
   ```

5. Add a `NavItem` in our `NavBar.js` that takes us to `/bakeries` and place it above the `/cookies` `NavItem`.

   ```jsx
   <NavItem className="nav-item" to="/bakeries">
     Bakeries
   </NavItem>
   <NavItem className="nav-item" to="/cookies">
     Cookies
   </NavItem>
   ```

6. Create a `BakeryItem` that takes `bakery` as a `prop`, and render the `image` of the bakery and the `name` as the `alt`.

   ```javascript
   import React from "react";

   const BakeryItem = ({ bakery }) => {
     return <img src={bakery.image} alt={bakery.name} />;
   };

   export default BakeryItem;
   ```

7. In `BakeryList`, `map` over your `bakeries` from `bakeryStore` and pass `bakery` as a `prop`. Don't forget to pass a `key`! Also don't forget to import `bakeryStore`!

   ```javascript
   const bakeryList = bakeryStore.bakeries.map((bakery) => (
     <BakeryItem bakery={bakery} key={bakery.id} />
   ));
   ```

8. Let's take a look at our bakeries. Nothing happened! Because `BakeryList` must be an `observer`.

   ```javascript
   import { observer } from "mobx-react";

   [...]

   export default observer(BakeryList);
   ```

9. Great, the images are appearing. Let's give it some styling touches. Create a `styles.js` file in your `BakeryList` folder and style your bakery items.

```javascript
import styled from "styled-components";

export const BakeryItemImage = styled.img`
  width: 20em;
`;
```

10. Let's also add a searching bar to our `BakeryList` component! Render `SearchBar`, set your `query` state and `filter` your `bakeries`.

```javascript
const [query, setQuery] = useState("");

const bakeryList = bakeryStore.bakeries
  .filter((bakery) => bakery.name.toLowerCase().includes(query.toLowerCase()))
  .map((bakery) => <BakeryItem bakery={bakery} key={bakery.id} />);
```
