# node-user-config
Read application settings from a configuration file with an environment variable fallback.

## Exmaple use
**user.config.json**
```json
{
  "mongoUrl": "mongodb://localhost/TestApp"
}
```

**index.js**
```javascript
const config = require('node-user-config');

// Will return mongoUrl property from user.config.json if the file exists 
//   or will search for an environment variable named MONGO_URL if not.
const mongoUrl = config.get('mongoUrl');  
```
