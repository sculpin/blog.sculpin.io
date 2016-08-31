---
title: "Deprecating Phar Distribution and Embedded Composer"

---

If you are currently using a globally installed phar distribution for Sculpin you should migrate to a per-project Composer installed version of Sculpin as soon as you can.

**TL;DR:** The most recent version of the Sculpin phar is extremely out of date, incompatible with PHP 7, and should be considered unavailable by October 1st. Upgrade your website project ASAP.

---

I have been putting this post off (and a few others) for six to twelve months. However, now that I am in a place where I can blog again, this is one issue that I need to address as quickly as possible.

## Any plans for Sculpin 3 would have required reworking the phar build and distribution process

In typical programmer fashion, I let myself get bogged down in the details of eventually needing to deploy Sculpin 3 phar builds rather than working on Sculpin 3. What little time I had to spend on Sculpin last year was sunk on solving this problem.

The build process has always been kinda hacky and, unfortunately, not kept under revision control.

I KNOW.

Lesson learned.

At some point last year I started working on this new deployment pipeline for building a phar that would be "major version aware." I didn't want `sculpin self-update` to bump people from Sculpin 2 to Sculpin 3 which turned out to be a weird and complicated problem to try and solve when you don't have a lot of time to throw at a project.

Not surprisingly, I didn't get far. After a few months of tinkering I realized I no longer had the ability to deploy a current version of the Sculpin to download.sculpin.io.

I don't want to go into the details on this as I'm quite embarrassed even sharing this much. At some point I needed to cut my losses on this part of the project and removed the instructions for installing Sculpin as a phar.

## The last officially available Sculpin phar is not compatible with PHP 7

One of my [lofty goals for Sculpin in 2015](/2015/03/02/the-sculpin-roadmap-for-2015) was for Sculpin 3 to support only PHP 7 out of the box.

Yeah, Sculpin 3 didn't happen.

To make matters worse, because Sculpin relied on Composer, and Composer relied on another library that was not compatible with PHP 7 (it had a class named `String`), this meant that you cannot run Sculpin 2 installed as a phar with PHP 7. At all.

## Maintaining phar distributions is hard, Sculpin or otherwise

Since I started distributing a phar for Sculpin I've been feeling a slight amount of pain with upkeep on maintaining the distribution of the phar.

It isn't awful, but it always felt hacky. Fragile.

I originally wrote Sculpin based off of bits and pieces I pulled from Composer. The self-update stuff was nice but felt haphazard and dangerous.

Composer's installer evolved over time but mine didn't. Trying to pull more pieces in and figuring out what changed, and how, was more work than I had time to do.

Since then, projects like Pádraic Brady's [PHAR Updater](https://github.com/padraic/phar-updater) have come out. Migrating to something like this would most definitely make things better but given the amount of time I've had to engage in Sculpin changes over the last year it didn't seem likely I'd get around to it.

If you're interested in what it would take to leverage Pádraic's project in a project like Sculpin (or your own project), Matthew Weier O'Phinney has a great tutorial on [Secure PHAR Automation](https://mwop.net/blog/2015-12-14-secure-phar-automation.html).

This isn't a request for someone to help, although [Georgiana Gligor](https://twitter.com/gbtekkie) has already offered to help fix the Sculpin phar build process and distribution. If we can find a way to automate the phar distribution *and it makes sense to do so*, I'm all for it. But is it worth it?

I guess the question comes down to who is using the phar distribution currently that do not already have Composer installed? And next, who doesn't have Composer installed and refuses to do so in order to continue using Sculpin?

## Composer is the best way to distribute Sculpin and support extensions

Sculpin was created to scratch an itch, tinker with distributing software as a phar, and to play with the idea of extending software by embedding Composer in an application.

Composer was still quite new when I got involved in the Composer project and started writing Sculpin. It wasn't clear then just how powerful Composer would become in its ability to distribute software over the following years.

As powerful as Composer has become, the idea of [Embedded Composer](https://github.com/dflydev/dflydev-embedded-composer) never took off. Not entirely. It is used by a handful of phar distributed projects, including Sculpin, but by and large even Sculpin users have been confused by this Embedded Composer thing.

The main problem I was never able to solve with Embedded Composer was the problem of dependencies changing within the phar over time and  being able to reconcile those with the installed dependencies on a project-by-project basis.

The magic of Embedded Composer is that on a project-by-project basis, an application like Sculpin could look at what the project wanted installed and resolve those dependencies against the dependencies that were already provided by the phar itself. Magic!

The downside of this is that it is only done once, at install time. Or again later at update time. But it isn't done automatically and certainly not done at runtime every time the application is run. Adding that functionality was potentially possible, but would it be worth it?

Imagine running `sculpin self-update` only to find out that Sculpin determined that it was no longer compatible with your project's custom extensions. Now imagine that you have to spend a bunch of time fixing your extension before you can use Sculpin again to build your site.

Blech.

Embedded Composer may still be useful in some cases, so I haven't decided to deprecate it entirely. But in the case of Sculpin, its time is limited.

## Migrating a phar managed site to a Composer managed site

The overall problem of the phar lagging master and PHP 7 issues was discussed at length in [issue #297](https://github.com/sculpin/sculpin/issues/297).

It was here that we formulated the migration path from a `sculpin.json` Sculpin phar managed site to a `composer.json` Composer managed site.

```
git mv sculpin.json composer.json
composer require sculpin/sculpin:^2.1@dev
```

Until Embedded Composer is finally removed from Sculpin, you will have to also require Embedded Composer:

```
git mv sculpin.json composer.json
composer require sculpin/sculpin:^2.1@dev dflydev/embedded-composer:^1.0@dev
```

You may then want to update `.gitignore` to ignore `/vendor/` instead of  `/.sculpin`

To see what it looked like to migrate the main Sculpin website to Composer managed, check out this commit: [sculpin/sculpin.io@889caa2](https://github.com/sculpin/sculpin.io/commit/889caa2dc0dddaf02f04d6dc99f9f45f73579f8d)

## Loose Ends

I'm slowing clawing back more time to work on Sculpin. The first things the team is going to focus on is cleaning up some loose ends like this so that Sculpin is more or less stable and installable for everyone by way of Composer.


