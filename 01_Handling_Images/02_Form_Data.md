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
  console.log(formData);
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
