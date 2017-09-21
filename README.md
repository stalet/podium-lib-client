# podlet-client

Client for fetching podium component fragments over http.


## Installation

```bash
$ npm i @podium/podlet-client --save
```

## General overview

TODO!


## Simple stream usage

Connect to a podium component server and stream the html content:

```js
const Client = require('@podium/podlet-client');
const client = new Client();

const component = client.register({
    uri: 'http://foo.site.com/manifest.json'
});

const stream = component.stream();
stream.on('error', (error) => {
    console.log(error)
})
stream.pipe(process.stdout);
```

## Simple fetch usage

Connect to a podium component server and fetch the html content:

```js
const Client = require('@podium/podlet-client');
const client = new Client();

const component = client.register({
    uri: 'http://foo.site.com/manifest.json'
});

component.fetch().then((content) => {
    console.log(content);
}).catch((error) => {
    console.log(error);
});
```


## Constructor

Create a new Podlet Client instance.

```js
const client = new Client(options);
```

### options (optional)

An options object containing configuration. The following values can be provided:

 * maxAge - {Number} - Default value, in milliseconds, for how long manifests should be cached. Default: Infinity
 * agent - {HTTPAgent} - Default HTTP Agent used for all requests.


## API

The Podlet Client instance have the following API:

### .register(options)

Registers a podlet.

Example:

```js
const Client = require('@podium/podlet-client');
const client = new Client();

const component = client.register({uri: 'http://foo.site.com/manifest.json'});
```

Returns a Podium Resource Object.

#### options (required)

The following values can be provided:

 * `uri` Uri to the manifest of a podium component  - Required


## Podium Resource Object

A registered Podium component is stored in a Podium Resource Object.

The Podium Resource Object contain methods for retreiving the content of a
Podium component. The URI to the content of a component are defined in the
components manifest. This is the content root of the component.

A Podium Resource Object has the following API:

### .fetch(options)

Fetches the content of the component. Returns a `Promise`.

### options (optional)

An options object containing configuration. The following values can be provided:

 * pathname - {String} - A path which will be appended to the content root of the component when requested.
 * query - {Object} - An Object which will be appended as query parameters to the request to the component content.

### .stream(options)

Streams the content of the component. Returns a `ReadStream`.

### options (optional)

An options object containing configuration. The following values can be provided:

 * pathname - {String} - A path which will be appended to the content root of the component when requested.
 * query - {Object} - An Object which will be appended as query parameters to the request to the component content.
