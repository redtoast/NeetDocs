# Internet API

Source: `_G.internet`

## Summary

Gives computers asynchronous http and web socket access, see [network events](/apis/events/network-events) for associated events.

## Functions

### GET(url, headers = {})
Sends a GET request to the given url with the supplied headers, which must be provided as strings.
Returns an id that can be used to identify the reply event.

`returns: Integer`

### POST(url, headers = {}, body = "")
Sends a POST request to the given url with the supplied headers and body.
Returns an id that can be used to identify the reply event.

`returns: Integer`

### CreateWebsocket(uri, headers = {})
Attempts to open up a new web socket. Default settings limit each computer to 5 websockets at a time. 
Unlike the other http functions, CreateWebsocket can throw errors directly. 
The functions for sending and closing websockets are enclosed in the successful opening event.
The id for CreateWebsocket is shared for ALL followup events relating to the socket, not just the initial reply.

`returns: Integer`

### hasAccess()
Checks if http access is allowed in the server config.

`returns: Boolean`

### isReady()
Checks if the computer is ready to send outgoing messages, returns false if the computer has reached the outgoing traffic limit set in server settings.

`returns: Boolean`