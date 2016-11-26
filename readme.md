# Auto generated Express documentation

## to create documentation:
### create file docks.js:
```
const Docs = require('express-api-doc');
const app = require('./app'); // your app.js
const docs = new Docs(app);
docs.generate({
  path:     './public/template.html',
});
```
### then run
```
node ./docks.js
```
### in *./public/* will be generated *template.html*

### now you can simply open it, or create route like this:
```
const express = require('express');
const router = new express.Router();
const path = require('path');

router.get('/api/doc', (req, res) => {
  res.sendFile(path.resolve('public/template.html'));
});

module.exports = router;
```
### so documentation will be available on http://your_host_name:your_port/api/doc

## if you have some coverage tests you can track requests and responses. For this change your app.js:
```
...
const Docs = require('express-api-doc');
...
const app = express();
const dock = new Docs(app);
...
dock.track({
	path: './public/examples.txt', // responses and requests will save here
});
app.use(favicon(path.join(__dirname, 'public', 'favicon.png')));
...

```
### now change you docks.js:
```
const Docs = require('express-api-doc');
const app = require('./app'); // your app.js
const docs = new Docs(app);
docs.generate({
  path:     './public/template.html',
  examples: './public/examples.txt,
});
```

### then you can run tests with generating documentation. For instance:
```
./node_modules/.bin/mocha -r should &&  node ./docks.js
```

### note! dock.track function must run before any declaration like this:
```
app.use('/', index);
```

## in generated html present list of avalible routes with search and sendbox, where you can try to send json to your server. Also under sendbox present list of examples, where you can see request and response json which has been tracked during tests.
