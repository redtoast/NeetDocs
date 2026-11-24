# Network Events

Events related to both local and http network activity.

See also
- [Internet API](/apis/internet)
- [IO API](/apis/IO)
- [Access Point Peripheral](/peripherals/access-point)

### networkMessage [Network]

Received when another connected computer runs `io.broadcast(...)`, all data sent is abstract and not strictly defined.

| Parameters   | Type | Description                 |
|--------------|------|-----------------------------|
| Arguments... | Any  | Data send by other computer | 

### HttpResponse [Network]

An HTTP reply to GET or POST internet API requests.

| Parameters     | Type                           | Description          |
|----------------|--------------------------------|----------------------|
| ID             | Integer                        | Response Tracking ID | 
| Status Code    | Integer                        | HTTP Status Code     | 
| Status Message | String                         | HTTP Status Message  | 
| Headers        | {String : String}              | Reply Headers        | 
| Body           | String \| Binary String \| Nil | Content of the Reply | 

### WebsocketOpened [Network]

Signals the successful creation of a websocket by the internet API, and provides interaction handlers.

| Parameters    | Type     | Description           |
|---------------|----------|-----------------------|
| ID            | Integer  | Websocket Tracking ID | 
| Send Handler  | Function | Sends Websocket Data  | 
| Close Handler | Function | Closes the Socket     | 

#### send(body, binary)

Sends the given body to the websocket receiver, binary should be set if sending non-text data.

#### close()

Closes the websocket connection

### WebsocketClosed [Network]

Signals a websocket has been closed, by either this host or the server.

| Parameters | Type    | Description           |
|------------|---------|-----------------------|
| ID         | Integer | Websocket Tracking ID | 
| Error Code | Integer | Websocket Error Code  | 
| Reason     | String  | Reason for Closure    | 

### WebsocketMessage [Network]

Signals that a message has been received by a websocket.

| Parameters | Type    | Description            |
|------------|---------|------------------------|
| ID         | Integer | Websocket Tracking ID  | 
| Body       | String  | Content of the Message | 
| Binary     | Boolean | If the Body isn't Text | 

### WebsocketSendSuccess [Network]

Signals a message has been successfully sent to the websocket.

| Parameters | Type    | Description           |
|------------|---------|-----------------------|
| ID         | Integer | Websocket Tracking ID | 

### WebsocketSendFailure [Network]

Signals a failure to send a message to the websocket.

| Parameters | Type    | Description           |
|------------|---------|-----------------------|
| ID         | Integer | Websocket Tracking ID | 
| Reason     | String  | Reason for Failure    | 