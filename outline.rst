WSGI without the Web
====================

* (2 minutes) Hello and About Me
* (5 minutes) The Challenge
  - Our microservices architecture
      ~ brokered message-passing infrastructure
  - The Scala solution
    ~ A custom DSL inspired by Scalatra
    ~ Actor-model concurrency
  - Desire for Python support
    ~ Performance/complexity spectrum
    ~ Rapid prototyping
    ~ Leverage developer knowledgebase
    ~ What if we could use off-the-shelf frameworks?
* (8 minutes) About WSGI
  - What it is
    ~ A PEP (PEP 3333)
    ~ an interface
    ~ for framework/middleware developers (not app developers)
  - What it isn't
    ~ Another protocol
    ~ Another web framework (for application developers)
  - (5 minutes) The life and times of a WSGI request/response
    ~ Web server receives frame off of the wire
    ~ Web server parses the request into an ``environ`` dictionary
    ~ Web server calls application, passing ``environ`` and ``start_response``
    ~ Application begins processesing request and formulating response
    ~ Application calls ``start_response``, passing the status code and the headers
        * ``start_response`` must return a ``write(body_data)`` callable, but this is considered
          legacy feature
    ~ Application must return an iterable of bytestrings
    ~ Server begins sending response, including the stored response code and headers, once the
      iterable returns its first non-empty bytestring
* (9 minutes) Our [W]SGI solution
    ~ A WSGI server that binds to ActiveMQ (using stompest) instead of a normal TCP socket
    ~ Things that didn't quite fit
        * Some ``environ`` variables (SERVER_NAME, SERVER_PORT, SERVER_PROTOCOL, wsgi.url_scheme)
        * Chunked responses
    ~ Handling the NOTIFY verb
    ~ Compared to the (theoretical) servlets solution
    ~ Pluggable concurrency model (reactors)
    ~ Demo???
* (1 minute) Takeaways
  ~ WSGI isn't scary: consider building your own server or middleware
  ~ WSGI doesn't have to use HTTP
* (5 minutes) Closing and Questions
