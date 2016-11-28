# Auto generated express documentation

### Create documentation:
__run__:
```
const Docs = require('express-api-doc');
const app = require('./app'); // your app.js
const docs = new Docs(app);
docs.generate({
  path:     './public/template.html',
});
```
__*template.html* will be generated in *./public/*__

### Track requests and responses:
__in app.js before routes declaration add:__
```
const Docs = require('express-api-doc');
const dock = new Docs(app);
dock.track({
	path: './public/examples.txt', // responses and requests will save here
});
```
__pass examples option to generate function:__
```
docs.generate({
  path:     './public/template.html',
  examples: './public/examples.txt,
});
```

in generated html present list of available routes with search and sendbox, 
where you can try to send json to your server. Under sendbox present list of examples,
where you can see request and response json which has been tracked (for instance during tests).

__you can change and generate your own template using [express-api-doc-template](https://github.com/forestlake/express-api-doc-template) project__
__to use your template, pass template option to generate function:__
```
docs.generate({
  path:     './public/template.html',
  examples: './public/examples.txt,
  template: './path/to/your/template.html',
});
```
__HINT: to publish you docs create route:__

```
router.get('/api/doc', (req, res) => {
  res.sendFile(path.resolve('public/template.html'));
});
```