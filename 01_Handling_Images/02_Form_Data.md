When uploading an image to the backend, we saw that all of our data is saved in `req.body`, while the image is in `req.file`. To create an object that has both, we will use `FormData`, which is a built-in JavaScript class.

1. In `createCookie`, create an instance of `FormData`.

   ```javascript
   createCookie = async (newCookie) => {
       try {
         const formData = new FormData();
   ```

2. Now we will add all of our data in `newCookie` to our instance `formData`. To do that we will loop over our `newCookie` object and `append` every property in `newCookie` to `formData`

   ```javascript
   createCookie = async (newCookie) => {
       try {
         const formData = new FormData();
         for (const key in newCookie) formData.append(key, newCookie[key]);
       }
   ```

3. Let's console log it.

   ```javascript
   try {
     const formData = new FormData();
     for (const key in newCookie) formData.append(key, newCookie[key]);
     console.log("formData", formData);
   }
   ```

4. Now, instead of passing `newCookie` to the `post` request, we will pass `formData`.

   ```javascript
   try {
     const formData = new FormData();
     for (const key in newCookie) formData.append(key, newCookie[key]);
     const res = await axios.post("http://localhost:8000/cookies", formData);
     this.cookies.push(res.data);
   }
   ```

5. Apply the same changes to `updateCookie` as well.

   ```javascript
   updateCookie = async (updatedCookie) => {
       try {
         const formData = new FormData();
         for (const key in updatedCookie) formData.append(key, updatedCookie[key]);
   ```

If you try to update a cookie's image, you'll notice that the image is not updated! You need to refresh to see the image. The reason for that is that we can't directly use the file the user passed, so we will convert it into a URL using a built-in function.

6. In `updateCookie`, after updating the data in the frontend, call the built-in method `URL.createObjectURL` which we will pass it the image file which is saved in `updatedCookie.image` and it will convert it into a URl. Then, we'll save this URL in `cookie.image`.

   ```javascript
   updateCookie = async (updatedCookie) => {
   try {
      // update in the backend
      const formData = new FormData();
      for (const key in updatedCookie) formData.append(key, updatedCookie[key]);
      await axios.put(
      `http://localhost:8000/cookies/${updatedCookie.id}`,
      formData
      );
      // update in the frontend
      const cookie = this.cookies.find(
      (cookie) => cookie.id === updatedCookie.id
      );
      for (const key in updatedCookie) cookie[key] = updatedCookie[key];
      cookie.image = URL.createObjectURL(updatedCookie.image);
   }
   ```
