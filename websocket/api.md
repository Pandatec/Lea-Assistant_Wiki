# Lea api websocket documentation

* [Text mode](#text-mode)
  * [Client messages](#client-messages)
  * [Server messages](#server-messages)

There is a websocket binding for HTTP API, enabling lower latencies through a stay alive connection.

Websocket for HTTP API is at: [wss://api.leassistant.com/api] on production

## Text mode

Both ends send messages in text mode. Each message is a JSON object.

## Client messages

### Request
- To send to the server to access any existing HTTP request
```ts
interface Request {
	id: number, // ID specified by client to identify the request that will be sent back in response
	token: string | undefined,  // JWT token to authentify, undefined if not logged in
	method: string, // HTTP method as specified by the standard: 'GET', 'POST', 'PATCH', 'DELETE', ...
	path: string, // full path to the request, withouts parameters: '/v1/auth/login', ...
	query: {[key: string]: string}, // request parameters in a map
	body: any // arbitrary object body
}
```

## Server messages

### Response
- Returned by server after each `Request` from client
```ts
interface Response {
	id: number, // same ID as in Request
	status: number, // HTTP status: 200, 404, 500, ...
	body: any // arbitrary body response
}
```
