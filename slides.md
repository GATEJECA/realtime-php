name: dblue
class: bg-dark-blue, center, middle
layout: true

<span class="twitter_id">@leggetter</span>

---

name: pink
layout: true

class: bg-pink, center, middle

<span class="twitter_id">@leggetter</span>

---

name: green
class: green-template, center, middle
layout: true

<span class="twitter_id">@leggetter</span>

---

name: black
layout: true
class: bg-black, center, middle

<span class="twitter_id">@leggetter</span>

---

name: white
layout: true
class: bg-white, center, middle, white-text

<span class="twitter_id">@leggetter</span>

---

template: dblue
class: title

# Real-time Web Apps & Symfony.
# What are your options?

* <span class="speaker">Phil @leggetter</span>
* <span class="speaker-job-title">Head of Developer Relations</span>
* <span class="speaker-nexmo-logo"></span>

???

---

template: white
class: bg-contain
background-image: url(./img/nexmo/what-nexmo-offers.png)

???

---

template: dblue
class: fixed-width-list

## What we'll cover

1. Why Real-Time?
2. What are your options
  * How do you choose?
  * Pros & Cons
3. 3 Example Solutions for PHP

---

template: dblue
class: bg-dark-blue, h1-big

# Why Realtime?

???

* Here are some examples of apps...

---

class: em-text, bg-cover, trans-h, bottom
background-image: url(./img/itv-news-nov-2015.gif)

# Notifications & Signalling

???

* Something has happened
* Changed
* Alert - do something

---

class: bg-cover, em-text, trans-h, bottom
background-image: url(./img/delighted-app.gif)

# Activity Streams

???

* a stream of activity
* things have - and are - happening
* synonymous with social apps
  * Twitter
  * Facebook
  * Google+
  * News
  * Sports

---


class: bg-cover, em-text, trans-h, bg-white, bottom
background-image: url(./img/senate-election-results.png)

# Data Visualizations

---

class: bg-video, trans-h, em-text, bottom

# Chat

<video id="video" autoplay="true" loop="true">
  <source src="./img/pie.mp4" type="video/mp4">
</video>

???

* The 101 of realtime
* An interactive experience
* Real-time matters

---

class: bg-white
background-image: url(./img/messaging-apps.png)

---

class: trans-h, bg-cover, bottom
background-image: url(./img/uber.jpg)

# Real-Time Location Tracking

---

class: trans-h, bottom, bg-cover
background-image: url(./img/atom-pair.gif)

# Multi-User Collaboration

???

* Google Apps
* Cloud 9
* TODO: other

---

class: bg-cover, trans-h, bg-white
background-image: url(./img/lunar-landing.png)

<h3 style="position: absolute; top: 2%; right: 2%; display: inline-block";>
  Multiplayer Games /<br />
  "Do some real-time art!"
</h3>

---

class: top

<img width="20%" src="./img/facebook.png" />
<img width="20%" src="./img/uservoice.png" />
<img width="25%" src="./img/google-docs.png" />
<img width="20%" src="./img/uber.png" />

--

# Users expect a real-time UX

--

# Without a real-time UX your app appears broken

---

template: dblue
class: h1-big

# Real-time Web Apps & PHP. What are your options?

---

class: h1-big

# 6 Factors to Consider

---

template: dblue
class: h1-big, bg-cover, em-text
background-image: url(./img/falkirk-wheel.gif)

# 1. Use an existing solution

## Don't reinvent the wheel

<small>Unless you've a unique use case</small>

---

class: fixed-width-list top

## Why use an existing solution?

* Fallback/upgrade hacks still required
--

* Support/Community
--

* Maintenance
--

* Future features
--

* Scaling

---

class: bg-white, bg-cover

background-image: url(./img/realtime-web-solutions-updated.png)

---

template: dblue
class: bg-cover, trans-h, top
background-image: url(./img/choose-a-lang.gif)

# 2. Use languages you're comfortable with

---

## Solutions by language

* **PHP**: ReactPHP, Ratchet, dNode-php, phpDaemon
* **Java**: Netty, Jetty
* **JavaScript (Node.JS)**: Faye, Socket.IO (Engine.IO), Primus.io
* **.NET (C#)**: SignalR, XSockets
* **Python**: Lots of options built on Tornado
* **Ruby**: em-websocket, Faye
* *Language agnostic*: most hosted services

---

# [j.mp/realtime-tech-guide](j.mp/realtime-tech-guide)

---

template: dblue
class: h1-big, trans-h, bg-contain
background-image: url(./img/windows-apple-android.jpg)

# 3. Native Mobile Support?

---

## Native Mobile Support?

* Only some have mobile libraries
* How much data are you sending?
* SSL required on 3/4G networks

---

## Solutions with Native Mobile Libraries

.left[* Faye
* Firebase
* Hydna
* PubNub]
.right[* Pusher
* Ratchet (via Autobahn)
* SignalR
* Socket.IO]

---

template: dblue
class: h1-big

# 4. Application/Solution<br />Communication Patterns

How does the client/server &amp; client/client communicate

???

Let me clarify this with code.

---

class: left-content, code-reveal, top wide

## Simple Messaging

```js
// client

var sock = new SockJS( 'http://localhost:9999/sockjs' );
```
--

```
sock.onmessage = function( e ) {
  console.log( 'message', e.data );
};
```
--
<hr />
```js
// server

sock.write( 'hello SockJS' );
```

---

class: code-reveal top wide

## PubSub

```js
// client

var client = new FayeClient();
```
--

```
client.subscribe( 'chat', function( message ) {
  // Handle Update
} );
```
--
<hr />

```js
// server

var message = {
  text: 'Hello, world!',
  user_name: '@leggetter'
}
Faye.publish( 'chat', message );
```

---

class: code-reveal top wide

## Evented PubSub

```js
// client

var pusher = new Pusher( APP_KEY );
```
--

```js
var channel = pusher.subscribe( 'chat' );
```
--
```js
channel.bind( 'message', function( data ) {
  // Handle Update
} );
```
--

```
channel.bind( 'message-updated', function( data ) {} );

channel.bind( 'room-name-changed', function( data ) {} );
```
--
<hr />

```js
// server

var data = [
  'text' => 'Hello, world!',
  'user_name' => '@leggetter'
}
pusher->trigger( 'chat', 'message', data );
```

---

class: code-reveal top wide

## Data Sync

```js
var myDataRef = new Firebase('https://yo.firebaseio.com/');
```
--

```
myDataRef.push( {name: '@leggetter', text: 'Yo!'} );
```
--

```
myDataRef.on( 'child_added', function(snapshot) {
  // Data added
});

myDataRef.on( 'child_changed', function(snapshot) {
  // Data has changed
});

myDataRef.on( 'child_removed', function(snapshot) {
  // Data removed
});
```

???

* Manipulating collection of data
* Not dealing with Messages

---

class: top code-reveal long wide

## RMI

```js
// client

$.connection.hub.start(); // async

var chat = $.connection.chatHub;
```
--

```js
chat.client.broadcastMessage = function (name, message) {
  // handle message
};
```
--

```js
chat.server.send( 'me', 'hello world' );
```
--
<hr />

```csharp
// server

public class ChatHub : Hub
{
```
--

```csharp
  public void Send(string name, string message)
  {
```
--

```csharp
    // Call the broadcastMessage method to update clients.
    Clients.All.broadcastMessage(name, message);
  }
}
```

---

class: bg-white
background-image: url(./img/rtw-tech-decision-matrix-black.png)

---

class: bg-white
background-image: url(./img/rtw-tech-decision-matrix-apps-black.png)

???

  
---

class: bg-white
background-image: url(./img/rtw-tech-decision-matrix-solutions-white.png)

???
  
* SockJS - focus on simple connections
* Some solutions offer PubSub and data sync
* Dropbox - offer simple DataStore API
* Only know a few RMI options
* New solutions: Meteor, DerbyJS, SailsJS - maybe a new category for these?

---

template: dblue
class: h1-big

# 5. Architecture Considerations

---

class: fixed-width-list

## I wanna build a real-time PHP app
or
## I wanna add real-time to an existing PHP app

---

template: green
class: bottom
background-image: url(./img/realtime-web-stack-tight-integration-self-hosted.png)

### Self Hosted <small>(Tightly Coupled)</small>

???

* Less initial overhead - quick Integration
* As project grows complexity increases
* Updating request/response cycle may impact realtime functionality and vise-versa
* Likely that the web server is handling load of both standard HTTP and realtime i.e. WebSocket, Server-Sent Events, HTTP fallbacks

---

## PHP Self-Hosted options

* [React (PHP)](http://reactphp.org/)
  * Event-driven, non-blocking I/O with PHP.
* [Ratchet](http://socketo.me/) (Built on React PHP)
  * WebSockets, WAMP, PubSub samples. No HTTP Fallback
* [dnode-php (RPC/RMI)](https://github.com/bergie/dnode-php)
* [phpDaemon](http://daemon.io/)
  * Lots of examples. Most docs in Russian.

???

* Ratchet: WebSockets, WebSocket Application Messaging Protocol, PubSub examples and more. Not HTTP fallback

---

> Yes it’s possible but not common or probably recommended yet. There are some projects that are starting to do this by running the HTTP stack on React [...] but it’s very uncommon at this point in time

[Chris Boden](https://twitter.com/boden_c), Creator/Maintainer of React (PHP) & Ratchet

---

template: green
class: demo-splash bottom trans-h
background-image: url(./img/realtime-web-stack-integration-self-hosted-symfony-ratchet.png)

???
  
* Generally agreed that a loosely coupled architecture is going to be easier to change and maintain
* Your DB may even be message-queue-capable e.g. Redis.
* So you simply need to hook your realtime server into that
* Web App for HTTP
* Realtime for realtime functionality
* Scale-out realtime server in the same way as web server

--

### Self-Hosted Demo 1: Symfony + Ratchet <small>(Loosely Coupled)

---

class: wide

## Self-Hosted Demo 1 - Pro & Cons

.left[
**Pros**

* PHP
* Simple integration
* Standards-based
  * WAMP/Autobahn
  * JS, Android, iOS & more
]

.right[
**Cons**

* No HTTP fallback
* Low-level abstractions
* Different programming style
* You need to scale
]

---

template: green
class: bottom, trans-h demo-splash
background-image: url(./img/realtime-web-stack-integration-self-hosted-symfony-faye.png)

--

### Self-Hosted Demo 2: Symfony + Faye<br /><small>(Loosely Coupled)

---

class: wide

## Self-Hosted Demo 2 - Pro & Cons

.left[
**Pros**

* PubSub
* Connection fallback
* Redis Queue support
* Simple integration
]

.right[
**Cons**

* Not PHP(?)
* You need to scale
]

---

template: green
class: bottom, trans-h demo-splash
background-image: url(./img/realtime-web-stack-integration-hosted-symfony-pusher.png)

--

### Hosted Demo: Pusher

---

class: wide

## Hosted - Pros & Cons


.left[
**Pros**

* Simple & powerful
* Instantly scalable
* Managed & dedicated
* Direct integration into PHP
]

.right[
**Cons**

* 3rd party reliance
]

???

* Load-balancing connections
* Maintaining state of connections
* Synchronising data between nodes
* Mapping connections to users?
* Dedicated hosted service will offer :
  * Make things easier and faster  
  * Reduce scaling complexities
  * Natural loose coupling via an API
* Where is your value?
  * Features v Infrastructure

---

template: dblue

# 6. Self-Hosted v Hosted

## "Build vs. Buy"

---

class: bg-cover top trans-h
background-image: url(img/build-vs-buy.png)

## Build vs. Buy - Costs

<a style="position: absolute; top: 2%;" href="https://baremetrics.com/calculator">baremetrics.com/calculator</a>

---

template: dblue

## How do you choose?
### 6 Realtime Framework Considerations

1. Use an Existing Solution
2. Use a language you're comfortable with
3. Do you need native mobile support?
4. Simple Messaging, PubSub (Evented), RMI or DataSync
5. Architectural considerations
6. Hosted v Self-Hosted (Build vs. Buy)

---

# You need Real-Time!

## There are lots of options.

## Make the choice that's right for you.

## I hope this helps!

---

class: fixed-width-list

# Resources

* [Real-time Tech Guide](http://j.mp/realtime-tech-guide)
* [React (PHP)](http://reactphp.org/)
* [Ratchet (PHP)](http://socketo.me/)
* [Faye (Node/Ruby)](http://faye.jcoglan.com/)
* [Nexmo](https://www.nexmo.com)
* [LopiPusherBundle](https://github.com/laupiFrpar/LopiPusherBundle)
* [github.com/leggetter/realtime-php-examples](https://github.com/leggetter/realtime-php-examples)

---

template: dblue
class: title

## Real-time Web Apps & Symfony.</br>What are your options?

### Questions?

[leggetter.github.io/realtime-php](leggetter.github.io/realtime-php)

* <span class="speaker">Phil @leggetter</span>
* <span class="speaker-job-title">Head of Developer Relations</span>
* <span class="speaker-nexmo-logo"></span>
