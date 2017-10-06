# Internationalization on nodejs

NodeJS doesn't appear to support regular locale usage out of the box. 
Things like this won't work:

```javascript
var amount = 100000;
var formatted = amount.toLocaleString('nl-NL');
```

This should return '100.000' instead of the default english format of '100,000',
as thousands in nl-NL are separated by a dot instead of a comma.

To fix this, you need to install the node-icu module:
```bash
npm install node-icu --save
```

And to use it, you need to either pass an environment var:
```bash
NODE_ICU_DATA=node_modules/node-icu node app.js
```

Or a command line parameter:
```bash
node --icu-data-dir=node_modules/node-icu app.js
```

The debian/ubuntu precomiled binaries for nodejs are linked against libicu. If nodejs
is not linked against it, obviously this will not work.
