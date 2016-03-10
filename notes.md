# Demos:

## General setup

1. Get redis running: `redis-server`
2. Run Symfony app `php symfony/app/console server:run`
3. Get two browser windows up side-by-side
4. Have editor open with in `realtime-symfony-examples`
5. Have ngrok running for quick demos

## General code-show:

1. Show server
2. Show client
3. Show demo

## Ratchet

1. Show sample app working in two windows. Post message. Doesn't appear in other window - need to refresh or poll.

2. Let's use Ratchet. To do this we're doing to need Redis running. It is.

3. Let's publish the message we receive to Redis. Open `ChatController.php`

```
sym-redis
```

4. Show Ratchet code:

* bin/chat-server.php
* Creating a new chat instance
* Passing in to Ratchet WsServer so it can get WS events
* Creating a redis client to receive events from our symfony app
* Initing the Chat app with the Redis instance
* Some crazy stuff going on around `$server->loop` - we can let Ratchet handle that.
* In `Chat.php`:
  * Collect incoming WebSocket connections
  * Subscribe to `chat` channel
  * When we receive messages from Redis we send to each client
  
5. Show the demo by going to http://localhost:8000/chat/ratchet/ and show demo in two windows
  
## Faye

1. Since we've got a nice loosely coupled system we can actually swap out Ratchet for another solution and continue to use the Redis message queue. This time let's go with Faye by James Coglan. Faye is available for Node and Ruby. In this sample I'll use Node.

2. Talk through `faye/index.js`

3. Stop the Ratchet example and run `faye/index.js`

4. Navigate to http://localhost:8000/chat/faye/ and show demo in two windows

## Pusher

1. Finally, here's how to integrate a hosted service such as Pusher. In this case we don't need a message queue so we can kill that. And we don't need a second service. Pusher replaces both of these components.

2. Open up `ChatController.php` and replace the Redis queuing code with the Pusher code.

3. Navigate to http://localhost:8000/chat/pusher/ in both windows

4. Run ngrok -subdomain=nexmo 8000 and ask people to go to nexmo.ngrok.com/chat/pusher

## Nexmo

1. Call +39 0683 600 016
2. Add `$this->sendSmsToAll($message)`
3. In demo window type is message to send.
