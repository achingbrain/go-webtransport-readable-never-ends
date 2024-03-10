# webtransport-go readable never ends

Starts a [webtransport-go](https://github.com/quic-go/webtransport-go) echo
server on port 12345.

The server accepts incoming WebTransport sessions, waits for a bidirectional
stream to be opened on the session and pipes it back to itself.

The client connects to the server, opens a bidirectional stream, writes a single
message to the writable before closing it, then reads from the readable until it
ends.

The readable stream never ends.

## Usage

Clone this repo then:

* Install `go1.20` or later
* Install go deps with `go get`

## Node.js

* Run `npm start`
* You should see something like:

```console
% npm start

> go-webtransport-readable-never-ends@1.0.0 start
> node index.js

SERVER start
SERVER ready

Paste the following code into https://codepen.io/pen/?editors=0012 or simmilar:

(async function main ()  {
  console.info('CLIENT create session')
... more code here
```

* Paste the JS code into a https://codepen.io/pen/?editors=0012 or otherwise run it in a browser
* Ensure the browser console is visible
* See the browser output:

```
"CLIENT create session"
"CLIENT wait for session"
"CLIENT session ready"
"CLIENT create bidi stream"
"CLIENT get writer"
"CLIENT wait for writer"
"CLIENT write"
"CLIENT close writer"
"CLIENT read from stream"
"CLIENT got from stream" // [object Object]
{
  "done": false,
  "value": {
    "0": 0,
    "1": 1,
    "2": 2,
    "3": 3
  }
}
"CLIENT read from stream"
```

The readable end of the stream never ends. If it did, you'd see these extra
lines at the end:

```
//..other output
    "2": 2,
    "3": 3
  }
}
"CLIENT read from stream"
"CLIENT got from stream" // [object Object]
"CLIENT read stream finished"
```
