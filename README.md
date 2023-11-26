# Converting CRA to Vite

ref : https://dev.to/henriquejensen/migrating-from-create-react-app-to-vite-a-quick-and-easy-guide-5e72

### Issues when converting

### Malform URI

comment out the %PUBLIC_URL% , vite doesnt like that syntex
https://github.com/nuxt/nuxt/issues/13518#issuecomment-1397304949
https://github.com/vitejs/vite/issues/6482

### Index in the root:

Had to change script reference to index.jsx vs index.js

```javascript
<script type="module" src="/src/index.jsx"></script>
```

### Jsx syntax

```javascript
failed to parse source for import analysis because the content contains invalid JS syntax. If you are using JSX, make sure to name the file with the .jsx or .tsx extension.
/Users/ocampo/Documents/vscode/convert_cra_to_vite/src/index.js:11:22

9 | <React.StrictMode>
10 | <App/>
11 | </React.StrictMode>
| ^
12 | );
```

...to resolve read the error, change your file extensions to .jsx

### expected a string (for built-in components)

index.jsx:9 Warning: React.jsx: type is invalid -- expected a string (for built-in components) or a class/function (for composite components) but got: object.

```javascript
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  // <React> // doesn't like when you wrap App in react
  <App />
  // </React>
  // <div>hello</div>
);
```

to resolve, just have ReactDOM render App, remove the React App is nested in
