Sculpin's Blog
==============

This repository contains (almost) everything that makes up
[blog.sculpin.io](http://blog.sculpin.io).

Powered by [Sculpin](https://github.com/sculpin/sculpin). =)

&copy; 2015-2018 dflydev


Build
-----

Sculpin uses the PHP command line interpreter (included with most PHP
distributions and default installations) as well as PHP's Composer package
manager.

To fetch the dependencies, run `composer install`.

Then, run this command to generate the blog output:

    vendor/bin/sculpin generate --watch --server

Your newly generated clone of [blog.sculpin.io](https://blog.sculpin.io) is now
accessible at `http://localhost:8000/`.
