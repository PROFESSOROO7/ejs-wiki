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
