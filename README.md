# Socket.io for Processing

This library won't be maintained. Java is not in my wheelhouse but this library is an evening's worth of work to port the precompiled version to Processing. The original library was written by Naoyuki Kanezawa and lives here: https://github.com/socketio/socket.io-client-java

I have had this exact code working very well with nodejs applications.

## Installation

Download, extract and drop the output in your Processing's library folder, in Mac OS that is `~/Documents/Processing/libraries/` - make sure the name is `socketio`.

## Example

This is an example pde which connects to localhost on port 5000.

```java
import java.net.URI;
import java.net.URISyntaxException;

import io.socket.client.*;
import io.socket.emitter.*;
import io.socket.hasbinary.*;
import io.socket.backo.*;
import io.socket.parser.*;

// Socket
Socket socket;
String ws = "ws://localhost:5000";

JSONObject json;

void setup() {
  try {
    socket = IO.socket(ws);
  }
  catch(URISyntaxException e) {
    println(e);
  }
  socket.connect();
  socket.on(Socket.EVENT_CONNECT, new Emitter.Listener() {
    @Override
    public void call(Object... args) {
      println("Connected to server");
    }
  }).on(Socket.EVENT_DISCONNECT, new Emitter.Listener() {
    @Override
    public void call(Object... arg0) {
      println("Disconnected from server");
    }
  });
  // "message" could be anything that you specify in your server app
  socket.on("message", new Emitter.Listener() {
    @Override
    public void call(Object... args) {
      String tmp = args[0] + "";
      json = parseJSONObject(tmp);
      println(json);
    }
  });

}

void draw() {
  
}
```
