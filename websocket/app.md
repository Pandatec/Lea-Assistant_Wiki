# Lea /app WebSocket documentation

* [Text mode](#text-mode)
  * [Application messages](#application-messages)
  * [Server messages](#server-messages)

WebSockets are used for server to app asynchronous communication.

WebSocket for applications is at: [wss://api.leassistant.com/app] on production

## Text mode

Both ends send messages in text mode. Each message is a JSON object.

## Application messages

### login
- To call first when connection is opened, otherwise the server will close the connection within 5 seconds.
```js
{
  type: "login",
  email: `${user_email}`, // Email app is logged in
  token: `${access_token}`  // access_token returned by HTTP API on login for email
}
```

### enableLocation
- To request for receiving a patient location, call the following
  - Only one patient for this kind of data stream can be listened at a time by a /app client
  - On success, starts streaming `Location` messages
```js
{
  type: "enableLocation",
  patientId: `${patientId}` // PatientId to listen the location to
}
```

### disableLocation
- To stop receiving previously requested patient location, call
  - On success, stops streaming `Location` messages
```js
{
  type: "disableLocation"
}
```

### enableBatteryLevel
- To request for receiving a patient battery level and online status, call the following
  - Only one patient for this kind of data stream can be listened at a time by a /app client
  - On success, starts streaming `BatteryLevel` messages
```js
{
  type: "enableBatteryLevel",
  patientId: `${patientId}` // PatientId to listen the battery level/online status to
}
```

### disableBatteryLevel
- To stop receiving previously requested patient battery level and online status, call
  - On success, stops streaming `BatteryLevel` messages
```js
{
  type: "disableBatteryLevel"
}
```

### enableEvent
- To request for receiving a patient new events (including zone), call the following
  - Only one patient for this kind of data stream can be listened at a time by a /app client
  - On success, starts streaming `Event` messages
```js
{
  type: "enableEvent",
  patientId: `${patientId}` // PatientId to listen the new events (including zone) to
}
```

### disableEvent
- To stop receiving previously requested patient new events (including zone), call
  - On success, stops streaming `Event` messages
```js
{
  type: "disableEvent"
}
```

### enableCalendarEvent
- To request for receiving a patient calendar event data updates, call the following
  - Only one patient for this kind of data stream can be listened at a time by a /app client
  - On success, starts streaming `CalendarEvent` messages
```js
{
  type: "enableCalendarEvent",
  patientId: `${patientId}` // PatientId to listen the new events (including zone) to
}
```

### disableCalendarEvent
- To stop receiving previously requested patient calendar event data updates, call
  - On success, stops streaming `CalendarEvent` messages
```js
{
  type: "disableCalendarEvent"
}
```


## Server messages

### tokenAccepted
- Returned by server when connected. Means that previous `login` message has succeded.
```js
{
  type: "tokenAccepted"
}
```


### pairingAccepted
- Returned by server when current pairing has been accepted by device user
```js
{
  type: "pairingAccepted"
  data: `${patientId}`
}
```

### alreadyPaired
- Returned by server when current pairing has failed because already paired
```js
{
  type: "alreadyPaired"
}
```


### pairingDenied
- Returned by server when current pairing has been denied by device user
```js
{
  type: "pairingDenied"
}
```

### locationPosition
- Position update for currently listened patient, implicitely clears current error
  - Streamed by `Location`
  - Location is in GPS coordinates
```js
{
  type: "locationPosition",
  data: {
   lat: patientLatitude, // double
   lng: patientLongitude // double
  }
}
```

### locationDiag
- Set error explaining why position is not currently available
  - Streamed by `Location`
```js
{
  type: "locationPosition",
  data: `${diagnosticMessage}`
}
```
### `diagnosticMessage` states
| Value | Description 
|-|-|
| `"location_disconnected"` | Patient is offline |
| `"location_disabled"` | Patient did not enable location |
| `"location_unavailable"` | Location is not available on patient device |

### batteryLevel
- Battery level update for currently listened patient
  - Streamed by `BatteryLevel`
```js
{
  type: "batteryLevel",
  data?: batteryLevel   // undefined if unknown, otherwise number zero-normalized (0=empty, 1=full)
}
```

### isOnline
- Online status update for currently listened patient
  - Streamed by `BatteryLevel`
```js
{
  type: "isOnline",
  data: boolean   // true if online, false otherwise
}
```

### newEvent
- New event just performed by the patient being listened to
  - Streamed by `Event`
```js
{
  type: "newEvent",
  data: any   // Event, as returned by HTTP API
}
```

### newZoneEvent
- New zone event just performed by the patient being listened to
  - Streamed by `Event`
```js
{
  type: "newZoneEvent",
  data: any   // Zone event, as returned by HTTP API
}
```

### calendarEvent
- Data update for calendar events for the patient
  - Streamed by `CalendarEvent`
  - The source of the data update can be anything: vocal command, in-app update, etc
```js
{
  type: "calendarEvent",
  data: {
   type: "created" | "modified" | "deleted",
   id: string,    // Only if data.type === "deleted",
   event: any    // Calendar event as returned by HTTP API, only data.id if id is not supplied
  }
}
```
