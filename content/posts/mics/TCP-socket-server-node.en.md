---
title: "How to build a TCP socket server in NodeJS"
date: 2022-01-07T09:35:29-08:00
draft: false
tags: ["NodeJS"]
categories: ["Mics"]
---

Using net module in NodeJS to build a simple TCP socket server

<!--more-->

## Start a TCP server

```js
const Ner=require("net");
const server = Net.createServer();
server.listen(port, function(){
  console.log(`Server listening on ${port}`);
})
```

## Receive data from socket

```JS
server.on("connection", function (socket) {
  console.log("A new connection has been established.");
	// write data to socket
  socket.write("hello\n");
	
  socket.on("data", function (chunk) {
    let data=chunk.toString();
    // close socket
    socket.destroy();
  });

  // When the client requests to end the TCP connection with the server, the server
  // ends the connection.
  socket.on("end", function () {
    console.log("Closing connection by the client");
  });

  socket.on("error", function (err) {
    console.log(`Error: ${err}`);
  });
});
```

