lynx-express
============

Express Middleware for sending data to StatsD.

Please refer to the [Lynx](https://github.com/dscape/lynx) documentation for more in depth details for configuring
the Lynx StatsD Client.

Once your client is configured, it's pretty straight forward to configure lynx-express.

Installation:

```
npm install lynx-express
```

Configuration:

```javascript

// Import lynx and lynx-express
var Lynx = require('lynx');
var LynxExpress = require('lynx-express');

// Setup your Lynx StatsD client as normal, optionally passing a prefix (like 'express')
var metrics = new Lynx('localhost', 8125, {prefix: 'express'});

// Create the Express middleware passing in the Lynx StatsD Client you created
var statsdMiddleware = LynxExpress(metrics);

// Tell Express to use your statsD middleware
server.use(statsdMiddleware());
```

By default lynx-express will track the counts for each response code and a response time for the overall system.
What's more useful is to have timing for each route in your Express app.  lynx-express can be configured to give you
per-route timing by adding an option timeByUrl to the middleware constructor.
```javascript
server.use(statsdMiddleware({timeByUrl: true})}
```
