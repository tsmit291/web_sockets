# Set Up
These instructions go through how to set up your sockets either using an express generator, not using the express generator and within you client side angular code!

### Not using the Express Generator
In the command line:
```
npm init
npm install socket.io express -S
touch app.js
echo node_modules > .gitignore
```
Then open up your app.js and set up your socket:
```js
var Express = require('express');
var Socket = require('socket.io');
var http = require('http');
```
*Keep in mind that 'Express' and 'Socket' are capitalized above!*

Continue in the app.js...
```js
var app = Express();
var server = http.createServer(app);
var io = Socket(server);
```
So what's going on this last bit? First we define app, that's just setting up our express middleware. Then we create a http server that is going to use our express as middleware. And lastly we include the socket in on everything and let it use our Express server.

Now head into your package.json file and add a start key with the value 'nodemon app.js' to your scripts object so it looks something like this:
```
"scripts": {
  "start": "nodemon app.js",
  "test": "echo \"Error: no test specified\" && exit 1"
}
```
Once you've done that, go ahead and install nodemon in the command line...
```
npm install nodemon -D
```
Next your going to create a 'public' folder with an 'index.html' and 'main.js' file in there.
Now we have to tell our middleware where we're going to hosting our static sites. How do we do that?

```js
app.use(Express.static('public'));
```

Now let's get our localhost running and setup....remember how to do that?

```js
var port = 3000;
server.listen(port, function(){
  console.log('Now listening on port: ' + port);
})
```
**Question:** Why do we write 'server.use' instead of our normal 'app.use' here?

Next we have to bring in the socket CDN in our Index.html! Check which version of Socket.io you're using (in your package.json) and go grab that CDN!
I have version 1.4.5 here for you:

*https://cdnjs.cloudflare.com/ajax/libs/socket.io/1.4.5/socket.io.js*

Awesome! You can throw in a console.log in your main.js so you can make that's wired up too! Then let's start our server!
```js
npm start
```

CHECK IN: How is everything? Is your server running correctly? What about your console?

**Question:** Where do we go to manipulate our Client now? What about our Server?

- Your Client side is going to consist of your browser and your public folder files!
- Your Server side consists of your app.js and your running nodemon!


To debrief your index.html should look like...
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Socket Chat</title>
  </head>
  <body>
    Hello World
    <script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/1.4.5/socket.io.js" charset="utf-8"></script>
    <script src="main.js" charset="utf-8"></script>
  </body>
</html>
```

and your App.js should look like....
```js
var Express = require('express');
var Socket = require('socket.io');
var http = require('http');

var app = Express();
var server = http.createServer(app);
var io = Socket(server);

app.use(Express.static('public'));

var port = 3000;
server.listen(port, function(){
  console.log('Now listening on port: ' + port);
})
```

__ARE WE READY TO SET UP OUR FIRST SOCKET???__

Go back into your app.js and let's get your first socket set up!
```js
io.on('connection',function(socket){
  console.log('We are entering the chat room');
})
```

In your main.js write
```js
var socket = io();
```

That's it! How can I check if my socket exists? Where should I see my console.logs?!?! Does Chrome web tools allow me to see when a site is using web sockets?

**Google It!**

If you did things correctly, we should see 'We are entering the chat room' logged out on the server side, and if we go under chrome web tools -> Network -> WS and refresh our browser, we should see a web socket!

__You're Fully Set Up Now!__

*************

### If you use the Express App Generator
Generate your app!
```
express --git socket-chat
cd socket-chat
npm install
echo node_modules > .gitignore
```
Now we need to hook up our socket middleware. Because we're using the generator our socket code needs to go in our bin -> www folder right after we create our http server. So we can type in something like this...

```js
// this first line should already be there
var server = http.createServer(app);
// This is talking about the socket.js file you're about to make
var Socket = require('../socket');
Socket(server);
```

**Question:** Why did we have to hook up our socket in our www file instead of our app.js?

*The bin file is where the generator runs the http server, that is what you need access to in order to fire your sockets, otherwise in app.js you only have access to your app.*

Now create a socket.js file that lives in the main file structure, add this code...
```js
var Socket = require('socket.io');
module.exports=function(server){
  var io = Socket(server)
  io.on('connection', function(socket){
    console.log('Now entering the chat room');
  })
}
```
**Question:** What is happening here?

There we are actually setting up our socket! We require socket.io and set up our socket connection (io.on!)

Now that the server side of our socket is set up, let's work on the client side!

In your views folder, in layout.jade, go ahead and add your socket CDN and a connection to your main.js (in your public javascripts folder)

```html
body
  block content
  script(src='https://cdnjs.cloudflare.com/ajax/libs/socket.io/1.4.5/socket.io.js')
  script(src='/javascripts/main.js')
```

And now finally let's fire the socket function and get it running. In your main.js add
```js
var socket = io();
```

Start your nodemon, open your web tools and make sure your socket is there!

__You're Fully Set Up Now!__

*****
### Sockets in Angular
So now I'm using Angular on the front-end, and I want to use my socket! So how do I do that? We create a service.

```js
var app = angular.module('myApp', []);

app.controller('mainController', function($scope, socketService){
  var socket = io();
})

app.service('socketService', function($scope){

})

```

What is the difference between...
- $apply()
- $digest()

When should I be using each? 


<!-- ```js
app.controller('mainController', function($scope, myService){
  // var socket = io();
  $scope.numbers = [];
  // socket.on('number', function(number){
  //   console.log(number);
  //   $scope.numbers.push(number)
  //   console.log($scope.numbers.length);
  // })

  myService.on(function(number){
      $scope.numbers.push(number);
      $scope.digest();
  })
});

// DONT PUT YOUR SOCKET STUFF IN YOUR CONTROLLER!!! ^^^ CREATE A SERVICE INSTEAD!! vvv

// Services - a thing thats accessible everywhere, grabbing data from everywhere, singleton - only has one instance
// Factories - creating something new, creates a new instance

app.service('myService', function($scope){
  var socket = io();
  var callbacks = [];
  socket.on('number', function(number){
    callbacks.forEach(function(cb){
      cb(number)
    }
    return{
      on(callback){
        callbacks.push(callback)
      }
    }
  }
});

app.service('myService', function($scope){
  return io();
})
``` -->
