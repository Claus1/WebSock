# WebSock

[![PyPI](https://img.shields.io/pypi/v/websock.svg)](https://pypi.org/project/websock/)
[![Build Status](https://travis-ci.org/Kai-Bailey/websocket.svg?branch=master)](https://travis-ci.org/Kai-Bailey/websocket)

<img src="logo/WebSock.jpg" width="60%">

A lightweight, multithreaded WebSocket server written in Python. 

## Description

WebSock is a Python implementation of a WebSocket server. WebSock allows you to create real-time applications, such as chatrooms or stock dashboards, without having to implement all the low-level details specified in the WebSocket protocol. The server application is built using the [TCP socket module](https://docs.python.org/3/howto/sockets.html) provided by the python programming language and follows the latest version of the WebSocket protocol specification ([RFC 6455](https://datatracker.ietf.org/doc/rfc6455/)). The project was motivated by our desire to learn more about how data is transferred across networks while providing a useful tool for others to build on top of.

## Design
WebSock is designed to abstract the protocol details away and allow users to get their applications up and running quickly. It utilizes the python threading module to efficiently handle multiple clients at once.

## How to run

Install the library with:

```python
pip install websock
```

WebSock provides a simple API that makes it easy to integrate into any application. To use the server you must provide an implementation for any or all of the following methods:

```python
def on_data_receive(client, data):
    '''Called by the WebSocket server when data is received.'''
    # Your implementation here.

def on_connection_open(client):
    '''Called by the WebSocket server when a new connection is opened.'''
    # Your implementation here.
    
def on_error(exception):
    '''Called by the WebSocket server whenever an Exception is thrown.'''
    # Your implementation here.
    
def on_connection_close(client):
    '''Called by the WebSocket server when a connection is closed.'''
    # Your implementation here.

def on_server_destruct():
    '''Called immediately prior to the WebSocket server shutting down.'''
    # Your implementation here.
```

Then, simply import and instantiate a new WebSocketServer object. The server expects a host and port, as well as any of the above methods you have chosen to implement.

```python
import WebSocketServer

my_server = WebSocketServer.WebSocketServer(
    "127.0.0.1",
    8467,
    on_data_receive = on_data_receive,
    on_connection_open = on_connection_open,
    on_error = on_error,
    on_connection_close = on_connection_close,
    on_server_destruct = on_server_destruct
)

my_server.serve_forever()
```

## Author
* [Kai Bailey](https://github.com/Kai-Bailey) - Software engineering student at the University of Alberta.
* [Fraser Bulbuc](https://github.com/fbulbuc) - Software engineering student at the University of Alberta.

## References
* The latest official WebSocket protocol specification, [RFC 6455](https://datatracker.ietf.org/doc/rfc6455/).
* Mozilla has an abundance of information on web technologies including a section on [WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API).


## Future Development

* Integration of the [Autobahn test suite](https://github.com/crossbario/autobahn-testsuite) to verify protocol coverage.