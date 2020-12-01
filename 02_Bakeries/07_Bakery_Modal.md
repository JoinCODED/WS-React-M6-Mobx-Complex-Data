1. Create a `BakeryModal` component. The easiest way is to copy the `CookieModal` and fix the fields. Keep in mind that every bakery need two fields, `name` and `image` only.

2. Remove all extra fields, keep the name and image only. Also remove anything related to updating a bakery.

3. Now, how can we call it? Create an `AddBakeryButton.js` for your bakery button. When the button is clicked it will open the `BakeryModal`. The easiest way to create it is to copy the cookie's `AddButton` and modify the naming.

   ```javascript
   import { useState } from "react";
   import { BsPlusCircle } from "react-icons/bs";
   import BakeryModal from "../modals/BakeryModal";

   const AddBakeryButton = () => {
     const [isOpen, setIsOpen] = useState(false);

     const closeModal = () => setIsOpen(false);
     const openModal = () => setIsOpen(true);

     return (
       <>
         <BsPlusCircle className="float-right" size="2em" onClick={openModal} />
         <BakeryModal isOpen={isOpen} closeModal={closeModal} />
       </>
     );
   };

   export default AddBakeryButton;
   ```

4. Let's try creating a new bakery. Yes! It works!

After creating a bakery, if you visit it directly you'll get an error. That's because when a bakery is first created, it doesn't have a `cookies` field.

5. So in `CookieList`, we will give `cookies` a default value of an empty array.

```javascript
const CookieList = ({ cookies = [] }) => {
```

Now it works perfectly.
