---
title: "Sculpin 3 Alpha"
author:
  shortname: kevin
  name: Kevin Boyd
  twitter: beryllium9
---
Things are looking good for Sculpin 3.0. This long-awaited new version will
resolve some of the "bumps" of 2.x, making Sculpin easier to install, easier to
get started with, and updating it to the latest versions of its dependencies.

This will introduce some small backwards-compatibility breaks. Users and
maintainers of custom bundles are advised to test those bundles with Sculpin 3.0
as soon as possible to ensure that they are going to work.

**The main BC breaks are:**

1. PHP 7.2 is now the minimum version of PHP that Sculpin targets.

1. No more Phar, no more "Embedded" Composer. Regular Composer is now the
   recommended way to install Sculpin.

1. The `getAdditionalSculpinBundles()` method of custom Sculpin kernels must be
   type hinted to return `array`.

1. YAML front-matter is more sensitive. Special characters like colons can make
   things unhappy, so you may have to update older front-matter entries to put
   double-quotes around such strings.

Please report any issues you find to the [GitHub issues page for
Sculpin](https://github.com/sculpin/sculpin/issues).

Special Thanks to [lex111](https://github.com/lex111) and
[Xerkus](https://github.com/Xerkus), whose help has been invaluable in getting
Sculpin 3.0 ready to launch.

And on a sad note, please take a moment to remember [Luis Cordova (aka
cordoval)](https://github.com/cordoval). His contributions to the PHP community
are incalculable, and we all mourn his passing earlier this year.
