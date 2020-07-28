At the moment, the `image` field in our `CookieModal` form takes a string. We will change it so that it takes a file.

1. In `CookieModal`, change the image's input field type from `text` to `file` and remove the `value`. The `value` of an `input` tag of type `file` is `read-only`, so that means it has to be an **Uncontrolled Component**.

   ```jsx
   <div className="form-group">
     <label>Image</label>
     <input
       required
       name="image"
       type="file"
       className="form-control"
       onChange={handleChange}
     />
   </div>
   ```

2. Let's add an image and console log the event value to see what it gives us

   ```jsx
   <div className="form-group">
     <label>Image</label>
     <input
       required
       name="image"
       type="file"
       className="form-control"
       onChange={(event) => console.log(event.target.value)}
     />
   </div>
   ```

3. But since this is a file, it will be saved in `event.target.files`.

   ```jsx
   <div className="form-group">
     <label>Image</label>
     <input
       name="image"
       type="file"
       className="form-control"
       onChange={(event) => console.log(event.target.file)}
     />
   </div>
   ```

As you can see it gives you an array, that's because this input field can take multiple images. But we only want one image in this case! So we need to take the first index of `event.target.file` only. The problem is that we use one method to handle all our input fields! So we will create another method that handles the image only.

4. Create a method called `handleImage` that saves the first index of the event's file.

   ```javascript
   const handleImage = (event) =>
     setCookie({ ...cookie, image: event.target.files[0] });
   ```

5. Pass the method to the input's `onChange`.

   ```jsx
   <input
     name="image"
     type="file"
     className="form-control"
     onChange={handleImage}
   />
   ```

6. And we received our image file!
