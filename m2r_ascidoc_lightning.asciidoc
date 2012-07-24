Mongrel2
========
:author:    Robert Pankowecki
:copyright: Zed Shaw, Guillermo Freschi, Robert Pankowecki
:backend:   slidy
:max-width: 45em
:data-uri:
:icons:
:language: ruby
:pygments:


== Robert Pankowecki ???

image:/home/rupert/Dropbox/Photos/rupert_outside_bw.jpg[]
image:/home/rupert/Dropbox/drug/arkency.png[]
image:/home/rupert/Dropbox/drug/wroclawrb/krasnal.png[]
image:/home/rupert/Dropbox/drug/wroclawrb/logos/drug-logo-name-rect-sq.png[]

* twitter: @pankowecki (ask question during this talk)
* github:  @paneq
* blog:    blog.robert.pankowecki.pl

== Mongrel2

* webserver
* http 1.1
* notghing with mongrel1

== Async

* Other servers assume that every request is received by a browser, then sent to a backend, and then directly sent out to the client and that’s it.

* Mongrel2 assumes that there is a connected client, and it sends requests to backends, but it makes no assumptions about how those backends respond to the clients. All it requires is that the backend application send messages addressed to the client and it will write them on the socket.

* Because of this design, Mongrel2 can easily house both classic HTTP clients, keep-alive style HTTP client, chunked encoding responses, JSSockets, or WebSockets using the same code.

* out of request-replay ghetto (!!!)

== N:M

* target up to 128 connection with 1 message
* Mongrel2 is the only web server capable of sending one request from a browser to N backends at once, and then return the replies from these handlers to M browsers. Not exactly sure what you could write with that, but it’s probably something really damn cool

== Message Protocol (ZMQ)

* ZeroMQ: a language- and transport-mechanism-agnostic messaging system that does not require a centralized messaging server to operate.
* Using ZeroMQ lets Mongrel2 talk to a huge number of languages, operate within any kind of network architecture, and do it with a very simple communication model and API that 
most programmers can understand.
* Your handler runs the application in different process.

== Async uploads

* Request body saved as file
* notification when upload started and when finished
* Easy way for measuring upload progress

== *sockets

* flash json sockets
* flash xml sockets
* websockets (implemented in unreleased 1.8 version)

== m2r

* Mongrel2 <- (zmq/tnetstring/json) -> Handler (M2R)
* Handler <- (ruby) -> Rack
* Rack <- (ruby) -> Rails

== Call for action:

=== This slide:

* https://github.com/perplexes/m2r/wiki/Contributing

=== Read:

* http://mongrel2.org/features/
* http://mongrel2.org/static/mongrel2-manual.html (especially Chapter 5: Hacking)
* http://zguide.zeromq.org/page:all (At least chapters 1 and 2)
* https://github.com/perplexes/m2r/issues
* http://rack.rubyforge.org/doc/SPEC.html
* https://github.com/rack/rack/tree/master/lib/rack/handler
