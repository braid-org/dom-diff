# DOM Diffing and Synchronization over Braid-HTTP

Efficiently diff and synchronization a DOM, either locally or over the network via [Braid-HTTP](https://datatracker.ietf.org/doc/html/draft-toomim-httpbis-braid-http).  Sync multiple browser & server DOMs over the network, via Dom Diffs.  Collaboratively edit live HTML.  Create mashups of UIs, interoperating via Dom Diffs.

- Supports [Braid-HTTP 04](https://github.com/braid-org/braid-spec/blob/master/draft-toomim-httpbis-braid-http-04.txt) protocol
- Uses Tree-sitter for robust, incremental HTML parsing
- Implements DOM diffing algorithm over Tree-sitter
- Run it on server or client
- Developed as part of the [braid.org](https://braid.org) project

This library makes it easy to add collaborative HTML editing to your web applications, allowing multiple users to edit the same DOM structure in real-time.

## General Use on Server

Install in your project:
```shell
npm install @braidjs/dom-diff
```

Require the library, which adds the `serve_dom_diff` request handler to the global namespace, and use it to handle HTTP requests:

```javascript
require('@braidjs/dom-diff')

http_server.on("request", (req, res) => {
  // Your server logic...

  // Serve DOM diffing for this request/response:
  serve_dom_diff(req, res)
})
```

> Todo: explain what serve_dom_diff is going to do.  I believe there is a text resource somewhere... and then a HTML version of the resource... and it will ... read changes to one, and write patches to the other?

## Server API

`serve_dom_diff(req, res, options)`
  - `req`: Incoming HTTP request object.
  - `res`: Outgoing HTTP response object.
  - `options`: <small style="color:lightgrey">[optional]</small> An object containing additional options:
    - `key`:  <small style="color:lightgrey">[optional]</small> ID of HTML resource to sync with. Defaults to `req.url`.
  - This method handles Braid-HTTP requests for collaborative DOM editing.

## Client-side Usage

```javascript
// Initialize DOM diffing
await init_dom_diff()

// Create a DOM diff object
let dd = create_dom_diff(initialHtml)

// Get current HTML
let currentHtml = dd.get()

// Apply a patch
let diff = dd.patch(newHtml)

// Apply DOM diff to actual DOM
apply_dom_diff(domElement, diff)
```

## Client API

`init_dom_diff()`
  - Initializes the DOM diffing system, loading necessary dependencies.

`create_dom_diff(html)`
  - Creates a new DOM diff object for the given HTML.
  - Returns an object with methods:
    - `get()`: Returns the current HTML.
    - `patch(newHtml)`: Applies a patch and returns the diff.

`apply_dom_diff(dom, diff)`
  - Applies a diff to the given DOM element.
