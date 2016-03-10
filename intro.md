# Web Sockets

### What are Web Sockets?
Real time bi-directional connection between a Client and a Server! Up until now how does our client/server interaction go?
* The client sends a request to the server
* The server sends a response back to the client

...right?

Well now with web sockets we are establishing a persistent connection between the client and the server. Kind of like talking on the phone with someone. Both sides are now able to emit and listen (request and respond) with out waiting on the other. The server can continuously emit while the client merely listens, both can emit whenever, or neither have to!

### Examples
<!-- Only a few people should be on Jared's site at once, otherwise it will crash the server  -->
* Jared Cross g10: http://parasplat.jaredcross.com/#/
* Socket.io Demos: http://socket.io/demos/chat/

**Spend 5 minutes to find another site that uses web sockets!**

To check if a site is using a web socket:
Chrome Web Tools -> Network -> WS (web socket) and see if one exists!
<!-- Agar.io and Slack both do to show as in class examples! -->
### Socket.io
[Reading](https://davidwalsh.name/websocket):
This article describes web sockets and socket.io extremely well and since we will working with socket.io I highly suggest getting through it! It's not very long, maybe 5-10 minutes!
