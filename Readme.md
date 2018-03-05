[![Build Status](https://travis-ci.org/anycable/anycable-go.svg?branch=master)](https://travis-ci.org/anycable/anycable-go) [![Dependency Status](https://dependencyci.com/github/anycable/anycable-go/badge)](https://dependencyci.com/github/anycable/anycable-go) [![Gitter](https://img.shields.io/badge/gitter-join%20chat%20%E2%86%92-brightgreen.svg)](https://gitter.im/anycable/anycable-go)

# AnyCable-Go WebSocket Server

WebSocket server for [AnyCable](https://github.com/anycable/anycable).

**NOTE:** this is a readme for the upcoming 0.6.0 version. [Go to 0.5.x version](https://github.com/anycable/anycable-go/tree/0-5-stable).

## Installation

The easiest way to install AnyCable-Go is to [download](https://github.com/anycable/anycable-go/releases) a pre-compiled binary.

Or with [Homebrew](https://brew.sh/)

```shell
brew install anycable/anycable/anycable-go
```

Of course, you can install it from source too:

```shell
go get -u -f github.com/anycable/anycable-go
```

### Heroku

See [heroku-anycable-go](https://github.com/anycable/heroku-anycable-go) buildpack.

## Usage

Run server:

```shell
anycable-go --rpc_host=0.0.0.0:50051 --headers=cookie,x-api-token --redis_url=redis://localhost:6379/5 --redis_channel=anycable --host=0.0.0.0 --port=8080

=> INFO 2018-03-05T08:44:57.684Z context=main Starting AnyCable 0.6.0
```

You can also provide configuration parameters through the corresponding environment variables (i.e. `ANYCABLE_RPC_HOST`, `ANYCABLE_REDIS_URL`, etc).

For more information about available options run `anycable-go -h`.

### Throubleshooting

First, try to run `anycable-go --debug` to enable verbose logging.

The most common problem is using different Redis channels within RPC instance and `anycable-go`. Find the following line in the logs:

```
INFO 2018-03-05T08:44:57.695Z context=pubsub Subscribed to Redis channel: __anycable__
```

and make sure, that RPC server publishes messages to the specified channel.

### TLS

To secure your `anycable-go` server provide the paths to SSL certificate and private key:

```shell
anycable-go --port=443 -ssl_cert=path/to/ssl.cert -ssl_key=path/to/ssl.key

=> INFO 2018-03-05T08:44:57.684Z context=http Starting HTTPS server at 0.0.0.0:443
```

## Build

```shell
make
```

## Docker

See available images [here](https://hub.docker.com/r/anycable/anycable-go/).

## ActionCable Compatibility

Feature                  | Status
-------------------------|--------
Connection Identifiers   | +
Connection Request (cookies, params) | +
Disconnect Handling | +
Subscribe to channels | +
Parameterized subscriptions | +
Unsubscribe from channels | +
Performing Channel Actions | +
Streaming | +
Usage of the same stream name for different channels | +
Broadcasting | +
Remote disconnect | - (WIP)
[Custom stream callbacks](http://edgeapi.rubyonrails.org/classes/ActionCable/Channel/Streams.html) | -
[Subscription Instance Variables](http://edgeapi.rubyonrails.org/classes/ActionCable/Channel/Streams.html) | -

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/anycable/anycable-go.

## License
The library is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
