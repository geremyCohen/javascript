# YOU MUST HAVE A PUBNUB ACCOUNT TO USE THE API.
Create an account at http://www.pubnub.com/account

## The PubNub Network JavaScript Real-time SDK v3.4.3
http://www.pubnub.com - PubNub Real-time Push Service in the Cloud. 

The PubNub Network is a blazingly fast Global Messaging Service for building
real-time web and mobile apps. Thousands of apps and developers
rely on PubNub for delivering human-perceptive real-time
experiences that scale to millions of users worldwide. PubNub delivers
the infrastructure needed to build amazing Mobile, MMO games, social apps,
business collaborative solutions, and more.

## PubNub CDN JavaScript SDK

You may access the latest PubNub JavaScript SDK on The PubNub Network CDN.

```html
<script src=http://cdn.pubnub.com/pubnub-3.4.3.min.js ></script>
<script>(function(){
    var pubnub = PUBNUB.init({
        publish_key   : 'demo',
        subscribe_key : 'demo'
    });
})();</script>
```

>**NOTE:** SSL Mode requires a few extra steps: [SSL MODE](README.md#ssl-mode)

## Get Started Here

https://github.com/pubnub/javascript#simple-example -
See the simple working example.
However if you want to learn the basic code for send/receive,
see below here:

#### Basic Send
```javascript
PUBNUB.publish({
    channel : "hello_world",
    message : "Hi."
})
```

#### Basic Receive
```javascript
PUBNUB.subscribe({
    channel : "hello_world",
    message : function(m){ alert(m) }
})
```

## PubNub JavaScript Platforms and Languages

>**NOTE**: Start with the **WEB** directory as the default deployment choice
to target all browsers and mobile platforms.

| Directory   | Description of the Build                                     |
|:------------|--------------------------------------------------------------|
| examples    | Several Sample Web Apps.                                     |
| web         | All **Mobile** and **Desktop Browsers** 100% supported.      |
| modern      | Light-weight Build for **only the latest Browsers**.         |
| mobile      | Light-weight Build for **only the latest Mobile Apps**.      |
| titanium    | Appcelerator Titanium Build with example project code.       |
| node.js     | Node.JS SDK (CommonJS).  **sudo npm install pubnub**         |
| socket.io   | Socket.IO Framework support with examples and videos.        |
| phonegap    | PhoneGap Build.                                              |
| core        | Master Source Files are located here.                        |

It is a good idea to start with the **web** directory and work your way
further into the platform you are seeking if needed.
The **web** directory supports all legacy, modern and mobile web browsers.

Let's start off with a simple example of how to use the PubNub Network
JavaScript SDK using the **web** build.  It's as easy as `copy/paste`.

## SIMPLE EXAMPLE

>**NOTE:** Copy and paste this example into a *blank* HTML file.

```html
<div id=pubnub pub-key=demo sub-key=demo></div>
<script src=http://cdn.pubnub.com/pubnub-3.4.3.min.js ></script>
<script>

    // LISTEN
    PUBNUB.subscribe({
        channel : "hello_world",
        message : function(m){ alert(m) },
        connect : publish
    })

    // SEND
    function publish() {
        PUBNUB.publish({
            channel : "hello_world",
            message : "Hi."
        })
    }

</script>
```

## ADVANCED SUBSCRIBE CONNECTIVITY OPTIONS/CALLBACKS
```html
<div id=pubnub pub-key=demo sub-key=demo></div>
<script src=http://cdn.pubnub.com/pubnub-3.4.3.min.js ></script>
<script>(function(){
    PUBNUB.subscribe({
        channel    : "hello_world",                        // CONNECT TO THIS CHANNEL.
        restore    : false,                                // FETCH MISSED MESSAGES ON PAGE CHANGES.
        message    : function( message, env, channel ) {}, // RECEIVED A MESSAGE.
        presence   : function( message, env, channel ) {}, // OTHER USERS JOIN/LEFT CHANNEL.
        connect    : function() {},                        // CONNECTION ESTABLISHED.
        disconnect : function() {},                        // LOST CONNECTION (OFFLINE).
        reconnect  : function() {}                         // CONNECTION BACK ONLINE!
    })
})();
</script>
```

## FULL MULTIPLEXING (Single TCP Socket)

>Multiplexing enhances mobile performance and battery savings.

The PubNub Network today is the only vendor that supports real channel
multiplexing with a single TCP Socket.
With Multiplexing, you are able to subscribe to a group of channels
while conserving device resources and
improving performance of message delivery;
all with a single network connection.
It is easy to use multiplexing with any `3.4` client SDKs because
it is transparent and automatic!
Here is an example of using Channel Multiplexing in JavaScript:

#### Adding Channels - Just keep adding!

> You can continue to add channels with subsequent calls.

>**NOTE:** See the Multiplexing Example:
>[Multiplexing Test](web/tests/multiplexing.html)

```javascript
// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
// Setup your Receiver Function
// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
function receiver( message, envelope, channel ) { /*...*/ }

// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
// ADD ARRAY - You can add an array of channel names to connect.
// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
pubnub.subscribe({
    channel : ['chan1','chan2','chan3'],
    message : receiver
})

// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
// ADD LIST - You can add a comma separated list of channel names.
// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
pubnub.subscribe({
    channel : 'chan4,chan6,chan7',
    message : receiver
})

// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
// ADD ONE MORE - You can add one channel at a time.
// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
pubnub.subscribe({
    channel : 'chan8',
    message : receiver
})
```

#### Removing Channels

```javascript
// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
// REMOVE ARRAY
// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
pubnub.unsubscribe({ channel : ['chan1','chan2','chan3'] })

// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
// REMOVE LIST
// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
pubnub.unsubscribe({ channel : 'chan4,chan6,chan7' })

// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
// REMOVE ONE
// -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
pubnub.unsubscribe({ channel : 'chan8' })
```

That's it!  It's easy to take advantage of multiplexing.
If you have any questions please contact help@pubnub.com


## AES Cryptography

>**NOTE:** This cryptography is compatible with all other 3.4 PubNub SDKs!
Easily encrypt your PubNub messages using AES by setting a single flag
when you publish a message and subscribing as well.
Even better, this encryption works across all `3.4` PubNub clients,
meaning you can encrypt/decrypt across these environments.

You can now use PubNub AES256 Cryptograhpy with JavaScript and other
SDK languages easily by following this starting point for JavaScript.
We’ve worked hard to make sure that using AES encryption in PubNub is easy.
The complexity of encrypting and decrypting the data is built into
the free PubNub client libraries (since our libraries
are open source, you’re welcome to see how we did it).
To use AES encryption in PubNub, simply do the following:

```html
<script src=https://pubnub.a.ssl.fastly.net/pubnub-3.4.3.min.js></script>
<script src=https://pubnub.a.ssl.fastly.net/pubnub-crypto-3.4.3.min.js></script>
<script>(function(){
    var secure_pubnub = PUBNUB.secure({
        publish_key   : 'demo',
        subscribe_key : 'demo',
        ssl           : true,
        cipher_key    : 'my-super-secret-password-key'
    });

    secure_pubnub.subscribe({
        channel : 'my_channel',
        connect : send_hello,
        message : receive_hello
    });

    function receive_hello(hello) {
        alert(hello);
    }

    function send_hello() {
        secure_pubnub.publish({
            channel : 'my_channel',
            message : 'hello!'
        });
    }
    
    function get_encrypted_history() {
        secure_pubnub.history({
            channel: channel,
            limit: 15,
            callback: function(notifications) {
                console.log(notifications);
            }
        });
    }

})();</script>
```

## HISTORY AND HERE-NOW EXAMPLE
```html
<span onclick="hereNow()">Click Me for Here Now!</span>
<span onclick="history()">Click Me for History!</span>

<script>(function(){
    function hereNow() {
        PUBNUB.here_now({
            channel  : 'hello_world',
            callback : function (message) { console.log(message) }
        });
    }

    function history() {
        PUBNUB.history({
            count    : 10,
            channel  : 'hello_world',
            callback : function (message) { console.log(message) }
        });
    }
})();</script>
```

## SSL MODE
```html
<div id=pubnub ssl=on></div>
<script src=https://pubnub.a.ssl.fastly.net/pubnub-3.4.3.min.js></script>
<script>(function(){

    var pubnub = PUBNUB.init({
        publish_key   : 'demo',
        subscribe_key : 'demo',
        origin        : 'pubsub.pubnub.com',
        ssl           : true
    });

    pubnub.subscribe({
        channel  : 'my_channel',
        connect  : function() { /* ... */ },
        callback : function(message) {
            alert(JSON.stringify(message));
        }
    });

})();</script>
```

## HISTORY
```html
<div id=pubnub></div>
<script src=http://pubnub.a.ssl.fastly.net/pubnub-3.4.3.min.js></script>
<script>(function(){

    var pubnub = PUBNUB.init({
        publish_key   : 'demo',
        subscribe_key : 'demo'
    });

    pubnub.history({
        count    : 10,
        channel  : 'hello_world',
        callback : function (message) { console.log(message) }
    });

})();</script>
```


## REPLAY

Replay is an API that allows you to "replay" the events of a channel
as they happened before in the past.
Replay will repeat the message delivery sequence in sync with
the timeline as they occured.

>**NOTE:** You must have Storage/Playback enabled on your Account.

```html
<div id=pubnub></div>
<script src=http://pubnub.a.ssl.fastly.net/pubnub-3.4.3.min.js></script>
<script>(function(){

/* GENERATE CHANNEL */
var channel = PUBNUB.uuid()
,   pub_key = 'demo'
,   sub_key = 'demo'
,   out     = PUBNUB.$('pubnub-terminal-out')
,   p       = PUBNUB.init({ subscribe_key : 'demo', publish_key : 'demo' });

/* OPEN RECEIVE SOCKET */
p.subscribe({
    channel : channel,
    message : function(data) { console.log(data) },
    connect : start_replay
});

/* START THE MOVIE STREAM */
function start_replay() {
    p.replay({
        source      : 'my_channel',
        destination : channel,
        reverse     : true
    });
}

})();</script>
```

## PRESENCE

PubNub Network offers Channel Presence which
allows you to ask the question "Who's There?"
and get back an answer with list of users and the occupancy count.

```html
<div id=pubnub pub-key=demo sub-key=demo></div>
<script src=http://cdn.pubnub.com/pubnub-3.4.3.min.js ></script>
<script>(function(){
    PUBNUB.subscribe({
        channel    : "hello_world",                        // CONNECT TO THIS CHANNEL.
        message    : function( message, env, channel ) {}, // RECEIVED A MESSAGE.
        presence   : function( message, env, channel ) {   // PRESENCE
            console.log( "Channel: ",            channel           );
            console.log( "Join/Leave/Timeout: ", message.action    );
            console.log( "Occupancy: ",          message.occupancy );
            console.log( "User ID: ",            message.uuid      );
            /* message is = {
                    "action"    : "join",
                    "timestamp" : 1347946204,
                    "uuid"      : "6e08b25f-48c0-4e94-92d0-0778a8b6013d",
                    "occupancy" : 1
            } */
        }
        
    })
})();
</script>
```

## BACKFILL

PubNub Network offers automatic hot-memory backfill which pulls the full
queue from the message Network to provide a response filled with a
compressed GZIP payload up to the maximum size of your queue length.
The Default Queue size is 100 for basic PubNub Accounts.
Adding backfill to a truthy value on subscribe, you can pull up to the
last 100 messages off of an in-memory queue.
Note that this queue may not always return 100 messages and you may instead wish
to use PubNub Network History API to guarantee pulling all historical messages.

>If you need to increase your queue length, contact PubNub Network
at help@pubnub.com for larger queue length.

Notice that we are using `backfill : true` in
the `pubnub.subscribe` call below.

```html
<div id=pubnub></div>
<script src=http://pubnub.a.ssl.fastly.net/pubnub-3.4.3.min.js></script>
<script>(function(){

    var pubnub = PUBNUB.init({
        publish_key   : 'demo',
        subscribe_key : 'demo'
    });

    pubnub.subscribe({
        backfill : true,
        channel  : 'my_channel',
        callback : function(message) {
            alert(JSON.stringify(message));
        }
    });

})();</script>
```


## WebSocket Client Interface

Optionally PubNub offers you the full RFC 6455
Support for WebSocket Client Specification.
PubNub WebSockets enables any browser (modern or not) to support
the HTML5 WebSocket standard APIs.
Use the WebSocket Client Directly in your Browser that
Now you can use `new WebSocket` any time!

You will need to hit the right resource URLs.
Make sure to follow the examples below.

Here is a quick example providing an easy adapter:

```javascript
WebSocket  = PUBNUB.ws;
var socket = new WebSocket('wss://pubsub.pubnub.com/PUB/SUB/CHANNEL');
```

Alternatively you may directly access the PubNub WebSocket via:

```javascript
var socket = new PUBNUB.ws('wss://pubsub.pubnub.com/PUB/SUB/CHANNEL')
```

The following example opens a `new WebSocket` in
**WSS Secure Socket Mode** with **2048 Bit SSL** Encryption.

```html
<!-- Import PubNub Core Lib -->
<script src="https://pubnub.a.ssl.fastly.net/pubnub-3.4.3.min.js"></script>

<!-- Use WebSocket Constructor for a New Socket Connection -->
<script>(function() {

    /* 'wss://ORIGIN/PUBLISH_KEY/SUBSCRIBE_KEY/CHANNEL' */
    WebSocket  = PUBNUB.ws;
    var socket = new WebSocket('wss://pubsub.pubnub.com/demo/demo/my_channel')

    // On Message Receive
    socket.onmessage = function(evt) {
        console.log('socket receive');
        console.log(evt.data);
    }

    // On Socket Close
    socket.onclose = function() {
        console.log('socket closed');
    }

    // On Error
    socket.onerror = function() {
        console.log('socket error');
    }

    // On Connection Establish
    socket.onopen = function(evt) {
        console.log('socket open');

        // Send a Message!
        socket.send('hello world!');
    }

    // On Send Complete
    socket.onsend = function(evt) {
        console.log('socket send');
        console.log(evt);
    }

    console.log(socket)

})();</script>
```

#### To Disable SSL WSS Secure Sockets:

```html
<!-- NON-SSL Import PubNub Core Lib -->
<script src="http://pubnub.a.ssl.fastly.net/pubnub-3.4.3.min.js"></script>

<!-- NON-SSL Use WebSocket Constructor for a New Socket Connection -->
<script>(function() {

// Note "ws://" rather than "wss://"
var socket = new WebSocket('ws://pubsub.pubnub.com/demo/demo/my_channel')

})();</script>
```

## Using the PUBNUB init() Function

How to create a new instance of the PubNub Object directly in JavaScript.
To do this, simply follow this `init` example:

```html
<script src=http://cdn.pubnub.com/pubnub-3.4.3.min.js ></script>
<script>(function(){

    // INIT PubNub
    var pubnub = PUBNUB.init({
        publish_key   : 'demo',
        subscribe_key : 'demo',
        origin        : 'pubsub.pubnub.com',
        uuid          : 'myCustomUUID'
    })

    // LISTEN
    pubnub.subscribe({
        channel : "hello_world",
        message : function(m){ alert(m) }
    })
 
    // SEND
    pubnub.publish({
        channel : "hello_world",
        message : "Hi."
    })

})();</script>
```

>**NOTE:** You do not need to use the `<div id=pubnub>` DIV with this method!

## SUPER ADVANCED SETTINGS

#### WINDOWING AND MESSAGE ORDERING

>**NOTE:** Windowing is in favor of battery savings
and throughput. The effect is more bundled messages
better compression and faster response times.
Windowing is a good idea most of the time.

PubNub JavaScript library includes a `windowing` feature that will
automatically allow the PubNub Network the window time needed
to bundle, compress and optimize messages for high-throughput.
This means that if you specify a long window, you will be able to
receive significant performance improvements and optimized performance.
With high throughput applications 
(Apps that send many messages per second)
a long enough window will benefit in performance and will allow
the needed period for the PubNub Network
to order the message delivery and compress the response efficiently.

>**NOTE:** Windowing 1000ms will allow 100 messages
in a second to be bundled and compressed at optimal speeds.

```javascript
var pubnub = PUBNUB.init({
    windowing     : 1000,    // MILLISECONDS
    publish_key   : 'demo',
    subscribe_key : 'demo'
});
```

Windowing is a good idea! Please use it for improved network efficiency.

#### KEEPALIVE PING INTERVAL

>**NOTE:** The JavaScript library will automatically detect disconnects
in near real-time regardless of `keepalaive`.

There exists extra rare cases where `keepalives` are used
to detect disconnections of the network connection;
situations where a network cable was unplugged for example.
Optionally you may sacrafice bandwidth and reduce battery life
by lowering the `keepalive` value.
By reducing the `keepalive` you receive
greater precision to detect rare edge-case drops.
The Default `keepalive` is *60 seconds*.
**Reducing this value to 30 seconds will help detect 
only the rare edge-case network problems
sooner under rare network disruption situations.**
It is not a good idea to reduce this value lower.
If you need it lower more, you must contact PubNub first.
Again, the JavaScript library will automatically
detect disconnects in near real-time anyway,
so it is not necessary to reduce this value further.

```javascript
var pubnub = PUBNUB.init({
    keepalive     : 30,
    publish_key   : 'demo',
    subscribe_key : 'demo'
});
```

## BEST PRACTICES

#### MESSAGE DELIVERY vs. GUARANTEED MESSAGE DELIVERY

The PubNub Network is a high throughput and reliable messaging service.
Note however that PubNub is not a guaranteed delivery with full Read Receipt Transactions.
You can however use improved designs and best practices to ensure you increase reliability.
One method includes *High Windowing Length* which provides slight improvements.

>**NOTE:** Higher windowing lengths allow improved message delivery.

We recommend following a few best practices to achieve high frequency of message delivery.
First ensure you are checking the publish response code and re-sending 
the publish if an error code is returned.

There is an easy way to make sure you do not run into undelivered
messages due to high frequency of published.
Actually there are a few easy ways.
The first option is to make sure you don't publish too quickly.
Do this by limiting to one concurrent publish per channel.
This is achievable by waiting for the publish response before sending another message.

Use our Elastic Message options.
You should instead send a single large message rather than segment
messages into small packets you manually assemble them on the receiving client.

>**NOTE:** Turn on Elastic Message Sizes in your Customer Account: 
https://admin.pubnub.com/

Is it possible to ensure 100% messages are delivered?  **YES!**
The way to do this includes a Read Receipt Design Pattern.
You must allow the Receiver of a message to ACKNOWLEDGE that
a message was successfully received.
The Sender will continuously re-send the message; with a delay between each re-send.
This continues until an ACKNOWLEDGEMENT is received from the receiver.


## FORCE TRANSPORT FOR JSON(P) OR FLASH SOCKET MODE

It is important to note that the PubNub JavaScript SDK will
automatically select the **best** transport method.
However if you desire, you can change this...

If you desire, though it is not recommended, you may manually enforce
JSON(P) or Flash Socket transports.
It is simple to manually enforce these transport mechanisms if needed
though again it is not recommended unless you are deploying on 
specific platforms such as *Philips Embedded SmartTV* or *Opera Powered TV*
platforms which sometimes simply require certain interfaces to be enforced.

#### Require Flash Socket Transport Only Mode


>**NOTE:** The PubNub div is required for the Flash Socket.


```html
<div id=pubnub flash=true></div>
<script>
    var flash_socket = PUBNUB.init({
        publish_key   : 'demo',
        subscribe_key : 'demo',
        origin        : 'pubsub.pubnub.com'
    });
</script>
```

#### Require JSON(P) Transport Only Mode

This will enforce the JSON(P) Transport to be used only and
will avoid all other transport methods.


>**NOTE:** you must Exclude the PubNub div.


```html
<script>
    var pubnub = PUBNUB.init({
        jsonp         : true,
        publish_key   : 'demo',
        subscribe_key : 'demo',
        origin        : 'pubsub.pubnub.com'
    });
</script>
```
