# Using your Socket
There are only a few major commands when it comes to sockets...

### Socket.emit
__Sending Messages!__
The 'socket.emit' method allows you send your messages or 'talk' to the client or server. There are two arguments that are passed through, 1. The name of the event. 2. The data I'm passing through the event. Data can be in the form of a  string, array, objects, etc. Take your pick!

```js
socket.emit('myMessage', 'Hello new user!!');
```

### Socket.on
__Listening to Messages!__
In order to listen to or receive the messages being sent over the connection, we use 'socket.on'. Socket.on also takes two arguments, 1. The name of the event to listen for  2. The callback. In this case we're listening for the event 'myMessage', and we're just going to log the data coming through for now.

```js
socket.on('myMessage', function(data){
  console.log(data);
})
```

### Io.emit
__Sending a Message to ALL Clients__
Now what if I want to send a message to everyone in the chatroom? Kind of like how our @channel works in the Slack?
Here I would use 'io.emit'. Again, this method takes two arguments, 1. The name of the event 2. The data we're emitting.

```js
io.emit('toEveryone', 'Hackathon tomorrow, get excited!!');
```

We would most likely want to put that code in our server side and just have our client listen in on it with a socket.on!

### Socket.broadcast.emit
__Sending a Message to ALL Clients, BUT the initiator__
So wait...when I do an @channel in slack, it doesn't notify me of the message I just sent out right? If I want to send a message to everyone except myself as the initiator I'm going use 'socket.broadcast.emit'. Can you guess how many arguments this is going to take?  Can you guess what they are?

```js
socket.broadcast.emit('myEvent', 'My message!');
```

That's it! Those are your 4 major commands that you will be using! But here's a few more for you to explore on your own...


### Stretch
- `io.sockets.emit`
- `socket.join`
- `socket.leave`
- `io.sockets.in`
- `socket.broadcast.to`
- `io.close`

### Where does it go?
So where does my socket code live? Well your server side code is going to go into your io.on function like this:

```js
io.on('connection', function(socket){
  socket.on('foo', function(data){
    socket.emit('bar', data + data + data)
  })
})
```
What is this socket doing? On the event of 'foo' run this function that will emit the event of 'bar' with the following data.

And our client side code is going to live in our main.js, like this:

```js
var socket = io();
socket.emit('foo', 'Hello Server');
socket.on('bar', function(data){
  console.log(data);
})
```
So what are they both doing? What is my output going to be? Try putting this code in your files and see what happens :)

You're ready to build your first chat!
