## Basic setup

First, install EJS:

```sh
npm install ejs
```

In Express v4, a very basic setup using EJS would look like the following. (This assumes a `views` directory containing an `index.ejs` page.

```javascript
let express = require('express');
let app = express();

app.set('view engine', 'ejs');

app.get('/', (req, res) => {
  res.render('index', {foo: 'FOO'});
});

app.listen(4000, () => console.log('Example app listening on port 4000!'));
```

There are a number of ways to pass specific configuration values to EJS from Express.

## View options

This is the most straightforward method, although `view options` has not been a documented option to use with Express since version 2. Use `app.set` to set `view options`:

```javascript
app.set('view options', {delimiter: '?'});
```
This method works for all options, even those which cannot be safely passed along with data, like `root`. It also allows you to set EJS options once, in one place.

## Custom render function

This is somewhat less straightforward, but also works well -- completely overrides the render function:

```javascript
let ejsOptions = {delimiter: '?'};
app.engine('ejs', (path, data, cb) => {
  ejs.renderFile(path, data, ejsOptions, cb);
});
```
This method works for all options, even those which cannot be safely passed along with data, like `root`. It also allows you to set EJS options once, in one place.

## App locals

Any properties set on `app.locals` will get mixed in to the `data` object passed into a render call for the view engine, and those with names matching known opts properties will be passed to EJS as opts:

```javascript
app.locals.delimiter = '?'
```
This does allow you to set your EJS options in one place, but will not work for unsafe options like `root`.

## Passing opts with data

Any properties in the data object for a `render` call with names matching known opts properties will be passed to EJS as opts:

```javascript
app.get('/', (req, res) => {
  res.render('index', {foo: 'FOO', delimiter: '?'});
});
```
This approach means you have to pass EJS options in every single render call, and also does not work with unsafe options like `root`.