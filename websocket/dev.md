# Lea device websocket documentation

* [Text mode](#text-mode)
  * [Shared messages](#shared-messages)
  * [Server messages](#server-messages)
  * [Device messages](#device-messages)

Websockets are used for server to device asynchronous communication.

Websocket for applications is at: [wss://api.leassistant.com/app] on production

## Text mode

Both ends send messages in text mode. Each message is a JSON object.

## Shared messages

### error
- When something went wrong i.e. you didn't used the doc correctly
```js
{
  type: "error",
  data: `${error_message}`
}
```

## Server messages

### uptodate
- Following a version* request, indicates the device it is to the latest known version and can proceed
```js
{
  type: "uptodate"
}
```

### outdated
- Following a version* request, indicates the device software is obsolete software and shall not proceed any further
```js
{
  type: "uptodate"
}
```

### token
- Provides a new private identifier to the device
```js
{
  type: "token",
  data: `${device_token}`
}
```

### tokenAccepted
- Tells the device that it is logged in after sending a login message
```js
{
  type: "tokenAccepted"
}
```

### enableLocation
- Start the GPS and send location every N seconds 
```js
{
  type: "enableLocation",
  data: {
   delta: seconds // This is a float
  }
}
```

### disableLocation
- Stop the GPS, do not send location anymore
```js
{
  type: "disableLocation"
}
```

## Device messages

### versionAndroid
- Performs a check of software version: server will respond with either a `uptodate` or `outdated` message
```js
{
  type: "versionAndroid",
  data: `${device_android_version}` // usual format: "${major}.${minor}.${patch}"
}
```

### login
- Logs the device in using it's token
```js
{
  type: "token",
  data: `${device_token}`
}
```

### firstConnexion
- Requests a token when it doesn't have any
```js
{
  type: "firstConnexion",
  data: battery // This is a normalized float (only between 0.0 and 1.0)
}
```

### location
- Indicate device current position in GPS coords
```js
{
  type: "firstConnexion",
  data: {
   lat: latitude, // This is a float
   lng: longitude // this is a float
  }
}
```

### locationDisabled
- Can't immediately send location because not granted by user but will send as soon as available
```js
{
  type: "locationDisabled"
}
```

### batteryLevel
- The current level of the battery
```js
{
  type: "locationDisabled",
  data: battery // This is a normalized float (only between 0.0 and 1.0)
}
```
