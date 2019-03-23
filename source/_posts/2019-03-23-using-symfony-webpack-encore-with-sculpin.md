---
title: "Using Symfony Webpack Encore with Sculpin"
author:
    shortname: Rae
    name: Rae Knowler
    twitter: RaeKnowler
---

The [Sculpin Blog Skeleton](https://github.com/sculpin/sculpin-blog-skeleton) is a template for creating a blog with Sculpin. It's used in the [Get
Started](https://sculpin.io/getstarted/) tutorial on sculpin.io, making it an important part of the Sculpin experience for many users. Until recently,
the Blog Skeleton handled JavaScript assets by installing components via Composer. It's now been updated to use Symfony's
[Webpack Encore](https://symfony.com/doc/current/frontend.html) library instead.

Three of us at [Liip](https://www.liip.ch/en), [Christian Riesen](https://twitter.com/christianriesen), [David Buchmann](https://twitter.com/dbu) and
I, had a hackday to work on Sculpin. [Kevin Boyd](https://twitter.com/beryllium9) offered us some suggestions of where to start, one of which was the
move to Webpack: a more modern way of handling JS and CSS assets.

Of course, you *can* make a website without any JS at all, but even a simple website needs some styling to look nice. The Blog Skeleton, which isn't
meant to look fancy, uses jQuery, Bootstrap and HighlightJS as well as a little custom CSS. With more dependencies, keeping everything organised can
get difficult. Encore takes all your CSS and JS files, as well as their dependencies, and bundles them up into one of each that you can link
to in your HTML (or Twig) templates.

It was simple to install Encore and configure it to work with Sculpin's file structure. Now, anyone building their blog using the Blog Skeleton as a
base can add their own JS and CSS in the default files, add require statements for any external libraries they want to use, and run Encore. The
links in the base Twig template won't change, but the new code will all be included.

We also spent some time cleaning up the Sculpin documentation in several places:

- The Sculpin Blog Skeleton README is now as small as possible, only what's needed to get the app up and running.
- The [Basic Project](https://sculpin.io/documentation/basic-project/) page on sculpin.io had a lot of information removed that duplicated the Get
Started tutorial. Now it explains the basic concepts of Sculpin more clearly.
- Documentation for using Webpack Encore with Sculpin has been added in the Basic Project page as well.

These changes will make it easier to get started using Sculpin to build a modern static website.
