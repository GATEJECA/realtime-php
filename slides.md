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

# Real-time Web Apps & PHP.<br />What are your options?

<img src="./img/cloudconf.png" style="width: 25%;" />

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

## You Have Realtime Data

<img src="./img/cloudconf-2015.png" style="width: 25%" />

* Changes/Interactions = Realtime Data
* Analyse, Describe, Publish, Consume Data
* Use to Analyse your apps in real-time
* Build realtime features for your customers

---

template: dblue
class: fixed-width-list

## What we'll cover

1. Why Real-Time?
2. What are your options
  * 6 Factors to consider when choosing
3. 3 x Example Solutions for PHP
  * Pros & Cons

---

template: dblue
class: bg-dark-blue, h1-big

# Why Realtime?

???

* Here are some examples of apps...

---

class: em-text, bg-cover, trans-h, bottom
background-image: url(./img/twitter-notifications.gif)

# Notifications & Activity Streams

???

Notifications

* Something has happened /Changed
* Alert - do something

Activity Streams: 

* a stream of activity: past & new
* synonymous with social apps
  * Twitter, Facebook, Google+
  * News, Sports

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
background-image: url(./img/gdocs-collaboration.png)

# Multi-User Collaboration

???

* Google Apps
* Cloud 9
* TODO: other

---

class: top

<img width="20%" src="./img/facebook.png" />
<img width="20%" src="./img/slack.png" />
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

class: top

## Native Mobile Support?

* Only some have mobile libraries
--

* How much data are you sending?
--

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
class: h1-big top

# 4. Application/Solution<br />Communication Patterns

--

How does the client/server &amp; client/client communicate

???

Let me clarify this with code.

---

class: code-reveal top wide larger-code

#### Simple Messaging

```js
// client

var ws = new WebSocket('wss://localhost/');
```
--
```js
ws.onmessage = function(evt) {
  var data = JSON.parse(evt.data);
```
--
```js
  // ^5  
  performHighFive();
};
```
--

<hr />

```js
// server

server.on('connection', function(socket){
```
--
```js
  socket.send(JSON.stringify({action: 'high-5'}));
});
```

???

* Simplistic pattern
* Similar to WebHooks

---

class: code-reveal top wide larger-code

#### PubSub

```js
// client

var client = new Faye.Client('http://localhost:8000/faye');
```
--
```js
client.subscribe('/news', function(data) {
```
--
```js
  console.log(data.headline);
});
```
--
<hr />

```js
// server

server.publish('/news', {headline: 'Nexmo Rocks!'});
```

---

class: long wide code-reveal top larger-code

#### Evented PubSub

```js
// client

var status = io('/leggetter-status');
```
--
```js
status.on('created', function (data) {
  // Add activity to UI
});
```
--
```js
status.on('updated', function(data) {
  // Update activity
});
status.on('deleted', function(data) {
  // Remove activity
});
```
--

<hr />

```js
// server

var io = require('socket.io')();
var status = io.of('/leggetter-status');
```

--
```js
status.emit('created', {text: 'PubSub Rocks!', id: 1});
```
--
```js
status.emit('updated', {text: 'Evented PubSub Rocks!', id: 1});
status.emit('deleted', {id: 1});
```

---

class: code-reveal top larger-code long wide

#### Data Sync

```js
// client

var ref = new Firebase("https://app.firebaseio.com/doc1/lines");
```
--
```js

ref.on('child_added', function(childSnapshot, prevChildKey) {
  // code to handle new child.
});
```
--

```js

ref.on('child_changed', function(childSnapshot, prevChildKey) {
  // code to handle child data changes.
});

```
--

```js

ref.on('child_removed', function(oldChildSnapshot) {
  // code to handle child removal.
});
```
--

```js

ref.push({ 'editor_id': 'leggetter', 'text': 'Nexmo Rocks!' });
```

--

Framework handles updates to other clients

???

* Manipulating collection of data
* Not dealing with Messages

---

class: top code-reveal long wide larger-code

#### RMI

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

## Real-time Web Apps & PHP.</br>What are your options?

### Questions?

[leggetter.github.io/realtime-php](leggetter.github.io/realtime-php)

* <span class="speaker">Phil @leggetter</span>
* <span class="speaker-job-title">Head of Developer Relations</span>
* <span class="speaker-nexmo-logo"></span>
