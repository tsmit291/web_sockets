## Authentication

Web Sockets, like regular HTTP requests, are very easy to work with even outside of your app.  In the same way that developers can easily bypass client-side security by issuing cURL requests directly, malicious developers can easily make direct web socket connections to your application.

Two small examples of implementing auth with socket.io:

[Sockets With Mongo Examples](https://github.com/gSchool/socket-mongo-auth-examples)
Two small examples of how you can implement authentication with socket.io. Be sure to research the underlying technologies (JSON Web Tokens and socket-io-express-session) that these apps use!

So you'll need to add some sort of authentication to prevent that. Here are some links to get you started thinking about how to do that.

- https://auth0.com/blog/2014/01/15/auth-with-socket-io/ (old but good)
- https://facundoolano.wordpress.com/2014/10/11/better-authentication-for-socket-io-no-query-strings/ - complex
- https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications - mdn
