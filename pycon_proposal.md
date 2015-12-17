===================
Pycon Talk Proposal
===================

Title
-----
Web Server Gateway Interface (WSGI) without the "Web"

Category
--------
Web Frameworks

Duration
--------
I prefer a 30-minute slot

Description
-----------
WSGI is the standard interface that web servers use to communicate with web applications. This talk
will explore WSGI for those unfamiliar with it, and will describe a novel use of WSGI to enable
python microservices to communicate via a brokered message passing system (e.g., ActiveMQ) while
still using off-the-shelf web app frameworks (e.g., bottle) for rapid development.

Audience
--------
Web app and framework developers, Microservice developers, Webserver admins (including hobbyists)

Python Level
------------
Intermediate

Objectives
----------
Familiarity with WSGI and appreciation of its simplicity; Ideas for using WSGI in non-web environments

Detailed Abstract
-----------------
Web Services Gateway Interface (WSGI) is the standard python interface that web servers use to
communicate with web applications.  It is an elegantly simple interface, and this talk will explore
the specification for those who may not understand how it works or what its purpose is.  While most
developers won't be writing their own web frameworks, this understanding is still valuable for
several reasons:

* It will lead web application developers to a better understanding of how your framework interacts
  with the web server.
* It may help web application developers notice cases where using or even writing a WSGI middleware
  layer might be useful.
* It will help web server admins (including hobbyists) understand how the server delegates request
  handling to applications.

As a case study, we will look at how and why Adtran built our own simple WSGI server.  Our mostly
JVM-based microservices backend system uses a brokered message passing system (ActiveMQ) for communication
between the various microservices.  This provides a number of advantages over using regular HTTP calls:

* No need for a directory service
* Built-in simple load balancing
* Publish/subscribe semantics

However, the messages that we pass over the message system are still just HTTP.  When the desire came
to add support for microservices to be written in Python, we wanted our developers to be able to use
the web frameworks they were already familiar with.  We were able to accomplish this by writing a simple
WSGI server which just binds to a queue in ActiveMQ (using the excellent `stompest` library) instead of
listening for HTTP directly on a TCP socket.  This part of the talk will shed further light on WSGI by
examining what was necessary to make this solution work.

Outline
-------
* (2 minutes) Hello and About Me
* (5 minutes) The Challenge
  - Our microservices architecture
      + brokered message-passing infrastructure
  - The Scala solution
      + A custom DSL inspired by Scalatra
      + Actor-model concurrency
  - Desire for Python support
      + Performance/complexity spectrum
      + Rapid prototyping
      + Leverage developer knowledgebase
      + What if we could use off-the-shelf frameworks?
* (10 minutes) About WSGI
  - What it is
      + A PEP (PEP 3333)
      + an interface
      + for framework/middleware developers (not app developers)
  - What it isn't
      + Another protocol
      + Another web framework
  - The life and times of a WSGI request/response
  - WSGI middleware
* (7 minutes) Our [W]SGI solution
      + A WSGI server that binds to ActiveMQ (using stompest) instead of a normal TCP socket
      + Things that didn't quite fit
          * Some `environ` variables
          * Chunked responses
      + Handling the ActiveMQ's publish/subscribe
      + Compared to a (theoretical) servlets solution
      + Pluggable concurrency model
      + Code snippets (possibly demo?)
* (1 minute) Takeaways
  - An understanding of WSGI
  - WSGI isn't scary: consider building your own server or middleware
  - WSGI can be adapted to non-web applications
* (5 minutes) Closing and Questions

Additional Notes
----------------
* Based on advice linked from the [proposing a talk page](https://us.pycon.org/2016/speaking/talks/),
  I have narrowed the scope of this proposal to focus on our use of WSGI. However, if this focus
  seems too narrow, I could adjust the talk to address more broadly how Adtran has used python in
  our microservices architecture including deployment, orchestration, and testing.
* Slides for this talk will be written in html/css/javascript using [impress.js](https://github.com/impress/impress.js).
  You can see the title and intro slides [on github](http://nathanalderson.github.io/wsgi-talk). The
  slides will be served locally for the talk to avoid possible network issues.
* I have spoken many times for large groups internally at my company, and have presented in the past
  at a meeting of the [Huntsville Python User Group](http://www.meetup.com/hsv-py/), but this would
  be my first time speaking at a large conference such as Pycon. If accepted, I will likely present
  the talk at the Huntsville Python User Group prior to Pycon.
* Slides for my presentation at the Huntsville Python User Group can be found (on
  Github)[http://nathanalderson.github.io/pytest-talk].  That talk explored how the pytest library
  generates its awesome failure reports by rewriting your code.
* The outline includes a bullet that reads "Code snippets (possibly demo?)". At this point I could
  either show slides with code snippets to show what a python-based microservice looks like using
  our WSGI server (spoiler: it's just regular bottle code), or I could do a very quick (~2 minute)
  live demo by writing a simple "hello world"-style microservice.  I may prepare the demo but have
  the code snippet slides available as a fallback.  Any feedback on this is welcome.

Additional Requirements
-----------------------
Just a video link for my laptop (HDMI or VGA preferred), a podium, and a single microphone.
