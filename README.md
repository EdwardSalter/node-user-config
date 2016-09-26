# node-user-config
Read application settings from a configuration file with an environment variable fallback.

## Why?
I needed a simple way to specify some application configuration without it being checked in to source control.
Without file system access to the deployment server, environment variables are the best option for application variables whereas a simple `user.config.json` file is easier to deal with at development time.

## Install
```shell
npm install node-user-config
```

## How it works
This module will import a simple json file and act as a wrapper around that file.
If the file does not exist, an environment variable with a similar name will be returned instead.

### Rules
The default naming scheme for environment variables uses the following rules:
Given the following property name to lookup: `somePropertyName`
  - A property inside `user.config.json` names `somePropertyName` will be returned if found.
  - An environment variable named `SOME_PROPERTY_NAME` will be returned if not.
  - If no environment varialbe named `SOME_PROPERTY_NAME` exists, null will be returned.
  
### Overrides
If a second argument is specified to the `get` method, the name of the environment variable can be overidden.
#### Exmaple
```javascript
const mongoUrl = config.get('mongoUrl', 'MY_APPS_DATABSAE_URL');  
```
This will search the `user.config.json` file for the `mongoUrl` property but fallback to an environment variable named `MY_APPS_DATABSAE_URL` if not found.

### Error
If the third parameter passed to the `get` method is true, if no key has been found in the `user.config.json` file or in the fallback environment variable; an error will be thrown.

## Usage
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

## 
