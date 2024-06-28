# DOM Diffing and Synchronization over Braid-HTTP

This library provides a set of tools for efficient DOM diffing and synchronization over the Braid-HTTP protocol, enabling real-time collaborative editing of HTML content.

- Supports [Braid-HTTP](https://github.com/braid-org/braid-spec/blob/master/draft-toomim-httpbis-braid-http-04.txt) protocol
- Utilizes Tree-sitter for robust HTML parsing
- Implements DOM diffing algorithm over Tree-sitter
- Supports server-side handling of collaborative DOM editing
- Developed as part of the [braid.org](https://braid.org) project

This library makes it easy to add collaborative HTML editing to your web applications, allowing multiple users to edit the same DOM structure in real-time.

## General Use on Server

Install it in your project:
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
