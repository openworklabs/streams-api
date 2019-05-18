# Instructions

## Developing an application using a local instance of streams-api

As of now, we use a simple babel parser to transpile javascript. There is no hot-module-reloading.

To compile the code:

`npm run build`

Make sure to run this command after every code update to see the change take effect

Use `npm link`

In the root of `streams-api` repository, run `npm link`

In the same level of your directory as your `package.json`, run `npm link streams-api`

#### Install

`npm i -s streams-api`

#### Create a new StreamAPI instance:

```js
import StreamAPI from 'streams-api'

const streamAPI = new StreamAPI()
```

The `StreamAPI` constructor takes an optional `textile config` object to overwrite the default:

```js
// local textile config
const config = {
  url: 'http://127.0.0.1',
  port: 40600,
  config: {
    API: {
      HTTPHeaders: '*'
    }
  }
}

const streamAPI = new StreamAPI(config)
```

The default config is your local textile node.

## Create a Stream:

```js
const newStream = await streamAPI.createStream(streamName, streamType)
```

_params:_

- streamName (string): The name of the stream
- streamType (string): The type of stream (one of `'public'`, or `'private'`)

_returns:_

- a stream object (object)

## Fetching data

#### Get a list of users' streams:

```js
const streamList = await streamAPI.getStreams(peerId)
```

_params:_

- peerId (string) - a textile peerId

_returns:_

- an array of stream objects (array)

#### Get all events from an individual stream

```js
const streamEvents = await streamAPI.getStreamEvents(streamId)
```

_params:_

- streamId (string) - the ID associated with a stream (really the textile threadId)

_returns:_

- an array of stream events (array)

#### Get all comments associated with a particular stream event

```js
const streamEvents = await streamAPI.getStreamEvents(streamId)
```

_params:_

- streamEventId (string) - the hash associated with a stream event (really the textile block hash)

_returns:_

- an array of stream comments (array)

## Adding data to streams

#### Add a new file to a stream

```js
const updatedStream = await streamAPI.addFile(streamId, file)
```

_params:_

- streamId (string) - the ID associated with a stream (really the textile threadId)
- file (buffer) - the file to add to a stream

_returns:_

- an updated stream object (object)

#### Send a message in a stream

```js
const updatedStream = await streamAPI.sendMessage(streamId, messageObject)
```

_params:_

- streamId (string) - the ID associated with a stream (really the textile threadId)
- message ?

_returns:_

- an updated stream object (object)

#### Add a new comment to a stream event

```js
const updatedStream = await streamAPI.sendMessage(streamId, messageObject)
```

_params:_

- streamId (string) - the ID associated with a stream (really the textile threadId)
- comment ?

_returns:_

- an updated stream object (object)

## Subscriptions

The streams API can provide event listeners to hear and react to different types of events

## Invites

#### Send an invite to a peer

```js
const successfulInvite = await streamAPI.invite(streamId, peerId)
```

_params:_

- streamId (string) - the ID associated with a stream (really the textile threadId)
- peerId (string) - the peerID to invite

_returns:_

- successfulInvite (bool) - true if invite was successfully sent

#### Generate an external peer invite URL

```js
const inviteLink = await streamAPI.invite(streamId, peerId)
```

_params:_

- streamId (string) - the ID associated with a stream (really the textile threadId)
- peerId (string) - the peerID to invite

_returns:_

- inviteLink (string) - a one time URL the peerId can use to join a stream
