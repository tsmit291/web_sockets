# Using your Socket 

### Socket.on
### Socket.emit
### io.emit
### socket.broadcast.emit


- `io.sockets.emit`
- `socket.join`, `socket.leave`
- `io.sockets.in`
- `socket.broadcast.to`

Talk about Angular / Single-Page-App considerations like:

- `$apply` in the callbacks
- moving it to a service
- cleaning up events

## Exercise

Have half the class connect to one room directly to your computer (using your-hostname.local:3000) and the other half connect to a different room.  Watch as events stream in.

Then have students do the challenge for sending custom messages.
