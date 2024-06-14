---
created: 2024-06-14T14:29:42 (UTC +08:00)
tags: []
source: https://medium.com/@Samitha.DIlan/sse-vs-web-socket-vs-socket-io-9998b5a5a099
author: Samitha Dilan
---

# SSE vs Web Socket vs Socket IO. SSE | by Samitha Dilan | Medium

> ## Excerpt
>
> In Server Sent Events, It allows browser client to receives updates from a server over a HTTP connection without resorting to polling. SSEs are a one way communications channel. (from server to…

## **SSE**

In Server Sent Events, It allows browser client to receives updates from a server over a HTTP connection without resorting to polling. SSEs are a one way communications channel. (from server to client only)

We can use SSE when we have to update display data, but we don’t want to have to poll the server. (Send progress of some process / polling count)

> **Initiate SSE Connection**

1.  Client (browser) initiate the communications between client and server.
2.  Client creates a new JavaScript EventSource object with the URL of an endpoint which is expected to return a stream of events over time.
3.  The server receives a regular HTTP request from the client. The client expects a response with a series of event messages at arbitrary times. The HTTP response open until it has no more events to send, connection has been open long enough and can be considered stale, or until the client closes the initial request.

![](https://miro.medium.com/v2/resize:fit:339/1*5l-I77Leb7NssdIACVrYKA.png)

> **Message format**

The SSE standard specifies how the messages should be formatted, but does not mandate a specific payload type for them.

Each event has set of colon separated key/value pairs. Each pair terminated by a newline, and the event itself terminated by two newlines.

Here’s a template for a single event message:

```
<span id="772d" data-selectable-paragraph=""><strong>id: &lt;messageId - optional&gt;\n<br>event: &lt;eventType - optional&gt;\n<br>data: &lt;event data - plain text, JSON, ... - mandatory&gt;\n<br>\n<br>\n</strong></span>
```

- **id**: A unique ID for event (optional) and we can track the event using the ID. In the drop of connection, we can use the ID to determine which event we got last and request that the server stream events after the last one received.
- **event**: It specifies the type of event in the case where one event stream may have distinctly different event types. (optional)
- **data**: The body of message. There can be one or more data key/pairs in a single event message.

## **Web Socket**

Web Socket is a computer communication protocol, which providing persistent, [f](https://en.wikipedia.org/wiki/Full-duplex)ull-duplex communication channels over a single TCP connection. Connection limitations are no longer a problem since WebSockets represent a single TCP socket connection. It is distinct from HTTP. But it is compatible with the HTTP protocol and have lower overhead.

The client can establishes a WebSocket connection through a process known as the WebSocket handshake. This process starts with sending a regular HTTP request to the server by client. An **UPGRADE** header which is included in request informs that the client wishes to establish a WebSocket connection.

> Example request header

```
<span id="4c72" data-selectable-paragraph="">Origin: http://host.example.com<br>Connection: Upgrade<br>Host: host.websocket.example.com<br>Upgrade: websocket</span>
```

> Example response header

```
<span id="4f3e" data-selectable-paragraph="">HTTP/1.1 101 WebSocket Protocol Handshake<br>Date: Sat, 11 July 2020 13:41:24 GMT<br>Connection: Upgrade<br>Upgrade: WebSocket</span>
```

Handshake is completed now and initial HTTP connection is replaced by a WebSocket connection that uses the same underlying TCP/IP connection. At this point either party can starting sending data.

Data is transferred through a WebSocket as _messages_, each of which consists of one or more _frames_ containing the data you are sending (the payload). In order to ensure the message can be properly reconstructed when it reaches the client each frame is prefixed with 4–12 bytes of data about the payload. Using this frame-based messaging system helps to reduce the amount of non-payload data that is transferred, leading to significant reductions in latency.

## **Socket IO**

**Socket IO** is a JavaScript library built on top of WebSocket and other technologies. It can be used in NodeJS & based server frameworks for server-side

Socket IO also a allowing bi-directional communication. First, Socket.IO creates a long-polling connection and then, once this is established, it upgrades to the best connection method available. In most cases, this will result in a WebSocket connection.

So, in the best-case scenario, provided that:

- the browser supports WebSocket ([97%](https://caniuse.com/#search=websocket) of all browsers in 2020)
- there is no element (proxy, firewall, …) preventing WebSocket connections between the client and the server

> Bidirectional Communication in Socket IO

**Sending**

```
<span id="a5f9" data-selectable-paragraph="">socket.emit('event_custom', 'sample data1');</span>
```

**Receiving**

```
<span id="32bd" data-selectable-paragraph="">socket.on('event_custom', function (data){<br>    console.log(data)<br>});</span>
```

**Disconnecting**

```
<span id="792d" data-selectable-paragraph="">socket.on('disconnect', function (){<br>    io.emit('user disconnected')<br>    console.log('disconnected')<br>});</span>
```

## Comparison between SSE, Web Socket and Socket IO

**_SSE_**

- SSEs are mono-directional. Data communication only happens one-way from the server to the client
- SSE is limited to UTF-8.
- Both Internet Explorer and Edge do not yet support SSEs.
- SSE suffers from a limitation to the maximum number of open connections, which can be especially painful when opening various tabs as the limit is per browser is six.
- Automatic reconnection, event IDs and sending arbitrary events(the only SSE have).
- No trouble with corporate firewalls doing packet inspection.

**_WebSockets_**

- Full-duplex, bidirectional communication between client and server.
- WebSockets can transmit both binary data and UTF-8.
- More browsers support it natively than they support SSEs.
- When connections are terminated WebSockets don’t automatically recover
- WebSockets are able to detect a dropped client connection, whereas SSEs first need to send a message before detecting the same issue.
- Browsers older than 2011 don’t support WebSocket connections.
- Some enterprise firewalls with packet inspection have trouble dealing with WebSockets.
- WebSockets require more development effort than SSEs.
- Complex protocol than the SSE protocol.

**Socket IO**

- Library to work with WebSocket
- Event-based, bi-directional communication between web clients and server
- Automatic reconnection
- supports broadcasting
- supports fallback options
- It will automatically upgrade to WebSockets if possible

References
