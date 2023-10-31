[![npm version](https://badge.fury.io/js/resilient-ws.svg)](https://badge.fury.io/js/resilient-ws)

# Resilient Websockets

Based on [reconnecting-websocket](https://raw.githubusercontent.com/pladaria/reconnecting-websocket); provides:

- reconnection when the connection is lost
- automatic retries when the message cannot be sent (e.g. when the connection is lost)
- ping/pong to keep the connection alive

## Installation

```bash
npm install resilient-ws
```

OR

```bash
yarn add resilient-ws
```

OR

```bash
pnpm add resilient-ws
```

## Usage

```js
import { ResilientWS } from 'resilient-ws'

ResilientWS.create({
  url: '',
  onConnectCallback: () => {
    console.log(`Wow this is a websocket connection!`)
  },
  onDisconnectCallback: () => {
    console.log(`Wow this is a websocket disconnection!`)
  },
  onMessageCallback: (message) => {
    console.log(`Wow this is a websocket message!`, message)
  },
  onErrorCallback: (error) => {
    console.log(`Wow this is a websocket error!`, error)
  },
})
```

ResilientWS maintains a single instance. So you can import it anywhere and use it.

```js
import { ResilientWS } from 'resilient-ws'

const ws = ResilientWS.getInstance()

ws.send({
    message: 'Hello World!'
    attempt: 0,
    forceReconnect: false,
})
```

### Ping/Pong

By default, ping/pong is disabled. You can enable it by passing the config for ping/pong when creating your ResilientWS instance.

```js
import { ResilientWS } from 'resilient-ws'

ResilientWS.create({
  ...config,
  pingPongConfig: {
  enabled: true
    pingInterval: 10000,
    pingMessage: 'ping',
  },
})
```

### Configure the Reconnecting Websocket

You can configure the reconnecting websocket by passing the config for reconnecting websocket when creating your ResilientWS instance.

You can find the complete list of options [here](https://www.npmjs.com/package/reconnecting-websocket#available-options).

```js
import { ResilientWS } from 'resilient-ws'

ResilientWS.create({
  ...config,
  reconnectingWSOptions: {
    maxRetries: 5,
  },
})
```
