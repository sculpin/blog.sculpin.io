---
title: "Sculpin 3 Is Here"
author:
  shortname: kevin
  name: Kevin Boyd
  twitter: beryllium9
---
It's been a long time coming, but thanks to the intrepid efforts of
several contributors, Sculpin 3 is finally here.

This new release brings the project a bit more in line with modern PHP
features and introduces some new commands and parameters.

Shout out to the following folks for all of their contributions - thanks
for your help!

* [lex111](https://github.com/lex111) (Alexey Pyltsyn)
* [Xerkus](https://github.com/Xerkus) (Aleksei Khudiakov)
* [GawainLynch](https://github.com/GawainLynch) (Gawain Lynch)
* [dbu](https://github.com/dbu) (David Buchmann, from **[Liip](https://www.liip.ch/en)**)
* [ChristianRiesen](https://github.com/ChristianRiesen) (Christian Riesen, from **[Liip](https://www.liip.ch/en)**)

New in Sculpin 3:

* Supports PHP 7.2 and higher!
* The `generate` command now supports `--source-dir` and `--output-dir`
  parameters
* Create custom content types with the new `content:create` command
  * Generates a very basic skeleton of templates
  * Supports defining custom taxonomies (such as `tags` or `categories`
    or any other categorizations you need)
* Initialize a bare-bones set of `source/` files using the new `init`
  command

However, there are some changes that affect backwards compatibility.

* PHP 7.2 is the minimum PHP version that Sculpin 3 will run on
  * Also, some new return typehints may require custom bundles to have
    their method signatures updated.
* Changes to the `symfony/yaml` component mean that certain YAML front
  matter values will need to be enclosed in quotes, particularly if they
  contain colons.
* Changes to pagination mean that certain URLs, such as
  "/blog/page/2.html", will change to a folder (e.g., "/blog/page/2/").
  * A gist can be found here with a concept for providing HTML-based
    redirects for legacy pagination files: [https://gist.github.com/beryllium/a1b0be7b603486f5e39f869db8ff3484](https://gist.github.com/beryllium/a1b0be7b603486f5e39f869db8ff3484)
* Bundles that write to the `sculpin.output_dir` parameter should be
  updated to use the `sculpin.writer` service instead, in order to
  facilitate the `--output-dir` parameter.
* A number of core classes are now `final` and some methods have been
  moved to `protected` and `private` to help reduce the code's
  complexity.

If you encounter issues with the new release or have suggestions, please
use [GitHub Issues](https://github.com/sculpin/sculpin/issues) or the
comments below.

Enjoy!