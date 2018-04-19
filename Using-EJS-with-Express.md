## Basic setup

In Express v4, a very basic setup using EJS would look like the following. (This assumes a `views` directory containing an `index.js` page.

```javascript
let express = require('express');
let app = express();

app.set('view engine', 'ejs');

app.get('/', (req, res) => {
  res.render('index', {foo: 'FOO'});
});

app.listen(4000, () => console.log('Example app listening on port 4000!'));
```

There are a number of way to pass specific configuration values to EJS from Express.

## View options

This is the most straightforward method, although `view options` has not been a documented option to use with Express since version 2. Use `app.set`:

```javascript
app.set('view options', {delimiter: '?'});
```
This method works for all options, even those which cannot be safely passed along with data, like `root`.

## Custom render function

This is somewhat less straightforward, but also works well -- completely override the render function:

```javascript
let ejsOptions = {delimiter: '?'};
app.engine('ejs', (path, data, cb) => {
  ejs.renderFile(path, data, ejsOptions, cb);
});
```
This method works for all options, even those which cannot be safely passed along with data, like `root`.

