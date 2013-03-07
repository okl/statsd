StatsD [![Build Status](https://travis-ci.org/etsy/statsd.png?branch=backends-as-packages)](https://travis-ci.org/etsy/statsd)
======

A network daemon that runs on the [Node.js][node] platform and
listens for statistics, like counters and timers, sent over [UDP][udp]
and sends aggregates to one or more pluggable backend services (e.g.,
[Graphite][graphite]).

We ([Etsy][etsy]) [blogged][blog post] about how it works and why we created it.

Inspiration
-----------

StatsD was inspired (heavily) by the project (of the same name) at Flickr.
Here's a post where Cal Henderson described it in depth:
[Counting and timing](http://code.flickr.com/blog/2008/10/27/counting-timing/).
Cal re-released the code recently:
[Perl StatsD](https://github.com/iamcal/Flickr-StatsD)

Key Concepts
--------

* *buckets*
  Each stat is in its own "bucket". They are not predefined anywhere. Buckets
can be named anything that will translate to Graphite (periods make folders,
etc)

* *values*
  Each stat will have a value. How it is interpreted depends on modifiers. In
general values should be integer.

* *flush*
  After the flush interval timeout (defined by `config.flushInterval`,
  default 10 seconds), stats are aggregated and sent to an upstream backend service.


Installation and Configuration
------------------------------

 * Install node.js
 * Clone the project
 * Create a config file from exampleConfig.js and put it somewhere
 * Start the Daemon:

    node stats.js /path/to/config

More Specific Topics
--------
* [Metric Types](./docs/metric_types.md)
* [Graphite Integration](./docs/graphite.md)
* [Supported Backends](./docs/backends.md)
* [Admin TCP Interface](./docs/admin_interface.md)
* [Backend Interface](./docs/backend_interface.md)
* [Metric Namespacing](./docs/namespacing.md)


Debugging
---------

There are additional config variables available for debugging:

* `debug` - log exceptions and periodically print out information on counters and timers
* `debugInterval` - interval for printing out information on counters and timers
* `dumpMessages` - print debug info on incoming messages

For more information, check the `exampleConfig.js`.


Tests
-----

A test framework has been added using node-unit and some custom code to start
and manipulate statsd. Please add tests under test/ for any new features or bug
fixes encountered. Testing a live server can be tricky, attempts were made to
eliminate race conditions but it may be possible to encounter a stuck state. If
doing dev work, a `killall node` will kill any stray test servers in the
background (don't do this on a production machine!).

Tests can be executed with `./run_tests.sh`.


Meta
---------
- IRC channel: `#statsd` on freenode
- Mailing list: `statsd@librelist.com`


Contribute
---------------------

You're interested in contributing to StatsD? *AWESOME*. Here are the basic steps:

fork StatsD from here: http://github.com/etsy/statsd

1. Clone your fork
2. Hack away
3. If you are adding new functionality, document it in the README
4. If necessary, rebase your commits into logical chunks, without errors
5. Verfiy your code by running the test suite, and adding additional tests if able.
6. Push the branch up to GitHub
7. Send a pull request to the etsy/statsd project.

We'll do our best to get your changes in!

[graphite]: http://graphite.wikidot.com
[etsy]: http://www.etsy.com
[blog post]: http://codeascraft.etsy.com/2011/02/15/measure-anything-measure-everything/
[node]: http://nodejs.org
[nodemods]: http://nodejs.org/api/modules.html
[udp]: http://en.wikipedia.org/wiki/User_Datagram_Protocol


Contributors
-----------------

In lieu of a list of contributors, check out the commit history for the project:
https://github.com/etsy/statsd/graphs/contributors
