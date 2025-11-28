* HTTP is a protocol
* this protocol, up to version 1.1 (HTTP/1.1) is/was text based, human readable
* it is based on request and responses
* server receives requests from clients and responds to them accordingly
* request format:
    * request line
        * method (GET, POST, PUT, OPTIONS, PATCH, DELETE, ...)  -> indicate a type
            of the action to be performed, for example:
            * GET - fetch resource (as read only) and do not modify it (multiple calls grant the same result), cachable
            * POST - create a new resource (multiple calls create multiple resources)
            * PUT - replace a resource wholly (sending the same data has the same effect)
            * PATCH - partial update of the resource (treated as multiple calls grant the same result)
            * DELETE - removal of the resource (repeated calls return success even when resource is already gone)
            * HEAD - same as GET, but getting headers without body (for checking metadata)
            * OPTIONS - what does the server handle? (returns allowed methods)
        * path (/hello, /time, ...) -> what do i want to trigger with the specified method?
        * protocol version (HTTP/0.9, HTTP/1.0, HTTP/1.1/ HTTP/2.0)
    * headers -> contain information/metadata about the request (type of data, length, cache control, date, encoding, custom headers)
    * body -> contain additional info, like in POST methods
* response format:
    * protocol version (HTTP/0.9, HTTP/1.0, HTTP/1.1/ HTTP/2.0)
    * status code (200, 404, etc.)
    * status message that goes with the status code
    * headers
    * body (optionally) containing the fetched resource
* HTTP relies on TCP (HTTP is in the application layer of OSI - 7, TCP is the transport layer - 4)
* to prepare an HTTP server:
    * create a socket (OS allocates resources for it in the kernel)
    * set options for this socket (for debugging, for example, SO\_REUSEADDR, SO\_REUSEPORT)
    * bind this socket to a host (an address) and a port
    * make the socket listen (listen also specifies the limit of the awaiting
      connections to the socket in the OS queue)
    * block and wait for a connection from the client with the accept() call
    * accept will return an address and a socket of the client
    * recv data from the client socket (specify amount of bytes)
    * parse data (HTTP or some other protocol specific)
    * sendall (keep sending the response buffer, until all bytes are sent) back
* test with something like this (when on localhost:8080): curl http://localhost:8080/hello
* curl will convert the URI into a proper HTTP request byte-string
