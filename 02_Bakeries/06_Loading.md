Have you noticed that if you refresh the page while you're on the cookie's detail or bakery's detail pages, we get an error. Why is that?

That's because the data is being rendered before it's completely fetched! So we need to do some kind of conditioning for our routes.

1. First let's move all our routes to their own component, just to make the code easier to read. Create a component file called `Routes.js`.

2. Move all the `Routes` along with `Switch` to `Routes.js`.

```javascript
const Routes = () => {
  return (
    <Switch>
      <Route exact path="/">
        <Home />
      </Route>
      <Route path="/bakeries/:bakerySlug">
        <BakeryDetail />
      </Route>
      <Route path="/bakeries">
        <BakeryList />
      </Route>
      <Route path="/cookies/:cookieSlug">
        <CookieDetail />
      </Route>
      <Route path="/cookies">
        <CookieList />
      </Route>
    </Switch>
  );
};
```

3. Don't forget to move all the needed imports from `App` to `Routes`.

4. Render `Routes` in `App`. Don't forget to import it. OMG!! `App` looks so cute right now!

```javascript
return (
  <ThemeProvider theme={theme[currentTheme]}>
    <GlobalStyle />
    <NavBar currentTheme={currentTheme} toggleTheme={toggleTheme} />
    <Routes />
  </ThemeProvider>
);
```

5. In `App.js`, we'll add a condition, if it's true we will render some kind of loading page, else we will render our routes.

```jsx
{
  true ? <h1>Loadinggg</h1> : <Routes />;
}
```

But, what will our condition be? Basically, we want to make sure that all bakeries are fetched before rendering our `Routes`.

6. In `bakeryStore`, we will create a new property called `loading` and set its initial value to `true`.

   ```javascript
   class BakeryStore {
     bakeries = [];
     loading = true;

     [...]

   }
   ```

7. Don't forget to add it to the `makeObservable` method as an `observable`.

   ```javascript
   constructor() {
    makeObservable(this, {
      bakeries: observable,
      loading: observable,
      fetchBakeries: action,
    });
   }
   ```

8. Back to `App.js`, we will check `bakeryStore.loading`, if it's `true` we will render the `Loading`, else we will render our routes. Don't forget to import `bakeryStore`.

   ```jsx
   {
     bakeryStore.loading ? <h1>Loadinggg</h1> : <Routes />;
   }
   ```

Let's check our website, we have our `Loadinggg` text, but at some point when the data is received we need to turn it to `false`!

9. Now in `fetchBakeries`, after fetching the data from the backend **and** saving it in `this.bakeries`, we will set `this.loading` to `false`. So it will **only** be set to `false` when the data is received. Genius right?!

   ```javascript
   fetchBakeries = async () => {
     try {
       const response = await axios.get("http://localhost:8000/bakeries");
       this.bakeries = response.data;
       this.loading = false;
     }
   ```

10. Let's check the website. It's stuck on `Loading`! Why?? That's because `App` must be an `observer`. Don't forget to import `observer` from `mobx-react`.

    ```javascript
    export default observer(App);
    ```

11. Let's go to any bakery detail and refresh. Yaaas! No errors!

12. But if we go to cookie detail and refresh we get an error! That's because we need to add a `loading` property to the `cookieStore` as well`.

    ```javascript
    class CookieStore {
      cookies = [];
      loading = true;
    ```

13. Make it `observable`.

    ```javascript
    constructor() {
        makeObservable(this, {
          cookies: observable,
          loading: observable,
          createCookie: action,
          fetchCookies: action,
          updateCookie: action,
          deleteCookie: action,
        });
      }
    ```

14. Change your condition to check the `loading` in both stores.

```javascript
{
  bakeryStore.loading || cookieStore.loading ? <h1>Loadinggg</h1> : <Routes />;
}
```
