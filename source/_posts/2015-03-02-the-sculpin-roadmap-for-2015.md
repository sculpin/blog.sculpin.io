---
title: The Sculpin Roadmap for 2015
social_image: /assets/images/posts/2015-03-02-social.png

---

I have big plans for Sculpin in 2015. I'm throwing them out here now both so the community can be aware of what to expect in 2015 but also for a little bit of accountability from the community.

With the support of [the new members of the Sculpin organization]({{site.url}}/2015/02/23/meet-the-new-members-of-the-sculpin-organization/), it should be **a lot** easier!

## Sculpin 3

A stable release of Sculpin 3 will be available by the end of the year. This is an ambitious goal driven by several factors, mostly revolving around changing dependencies (and associated API changes) and changes being made directly to Sculpin's API.

## Symfony 3

Symfony 3 is [currently scheduled to be released by November of 2015](http://symfony.com/blog/symfony-3-0-the-roadmap). I'd like `master` to start tracking Symfony 3 as soon as possible. The earlier we start testing out any changes to how Kernel or Bundles behave the better chances we have at influencing some decisions on how Symfony 3 will work.

On the technical side, Sculpin is implemented as an application built around a Symfony Kernel. In Symfony 2, there was an assumption made that Kernel applications were by default going to be HTTP based. This was very much *not* the case for Sculpin. As such, we've had to make a lot of design tradeoffs to account for this.

While the tradeoffs were mostly just in unneeded dependencies, the application as a whole would make more sense if we could leverage a Kernel without the constraints or implications that it has anything at all to do with HTTP. [It didn't look like Symfony 3 was going to make these changes](https://github.com/symfony/symfony/issues/9406#issuecomment-27389672) but it *does* sound like Symfony 3 will be more split which could help clean things up a bit more. What this will look like is still a bit unclear to me.

This may have major implications on the API and structure of how Sculpin is built. If the Bundle system changes a lot this will require reworking almost all of Sculpin's internal wiring. And depending on any Symfony 2.x backward compatibility layer being available, it may result in major changes to anyone else who has built extensions (or used third-party extensions) that were written for Sculpin.

I've also considered abandoning Symfony Kernel as Sculpin 3's core if it turns out to be more trouble than it is worth. There have been huge advantages to using Kernel (didn't have to write my own bundle/extension layer) but it has come at a big cost. Symfony bundles are a barrier to entry for many people and if Kernel truly is [*never*](https://github.com/symfony/symfony/issues/9406#issuecomment-27389672) going to be usable outside of HTTP Kernel it might be best to rip the band-aid off sooner rather than later.

This could potentially be a big deal, so I'd like to get feedback on who is actively working with Sculpin-specific extensions or using any generic Symfony 2 bundles so that I can get a better idea what kind of impact this will have on the community.

Nothing has been decided yet, but this is looking to be the biggest change coming to Sculpin.

## Minimum Supported PHP Version

With Sculpin 3 the minimum supported PHP version will be bumped to PHP 7 *if there is a stable PHP 7 release available by the end of the year*. We'll be keeping an eye on the development of PHP 7 to see whether it will actually be ready in time to launch Sculpin 3 with support for PHP 7.

This is a major change over the previously supported PHP 5.3.2. Even now I'm only running PHP 5.5 on my local development environments so this will be huge for me as well.

Sculpin 2 will continue to work with PHP 5.3.2+ so people who are unable or unwilling to upgrade to PHP 7 will still be able to use Sculpin. However, I'd love to be able to help keep the PHP community moving toward using current and supported versions of PHP. As already hinted at, in the past I've been pretty horrible about this myself. Time to change that.

## Markdown, Markdown, Markdown

I have long had my eyes on replacing php/markdown with [Ciconia](https://github.com/kzykhys/Ciconia). However, I'm no longer certain that Ciconia is going to be the best choice. Or more accurately, the *only other best* choice. As [Phil Sturgeon](https://twitter.com/philsturgeon) has [written about extensively](https://philsturgeon.uk/markdown/2014/11/30/state-of-markdown/), there are many, many options when it comes to Markdown.

Some work has already been contributed to make it so that you can provide other Markdown implementations for Sculpin. However, I'd like to revisit this and see if there are other solutions that may work better.

There are many Markdown dialects available for PHP now so it is becoming more and more important for users of Sculpin to be able to choose the flavor that works for them.

## Documentation

The documentation for Sculpin has been a sore spot for me for quite some time. There is just enough information in the docs currently to get you in trouble. They need to be revamped in a big way so that they are more useful, for more people, more often.

Fortunately, Emma Jane is on the case. Helping to come up with a brand new set of documentation from the ground up will be one of her special projects this year. We'll let you know when we have more details so that if you have suggestions or requests for the documentation we can take them into consideration!

## Themes

This year we will make themes a first class citizen of Sculpin. There are a few lingering questions about how certain things should be handled but most of those questions are answered. The answer, however, was, "we have a lot of work to do."

**If you are currently working with the [WIP] theme support for Sculpin, know that there may be major changes to the theme system over the next year.**

## Testing

I am sad to say that Sculpin is far from my most tested piece of software. A little has been done here or there but for the most part Sculpin is manually tested by users everywhere.

This situation will change this year. New features and bug fixes will start to be accompanied by tests to start fleshing out Sculpin's test suite.

## Backwards Compatibility Concerns

### Sculpin Site Layout

I'm going to aim for keeping the basic site layout 100% backward compatible with Sculpin 2. This *may not* extend to configuration (more on that later) but it should be a high priority for us that a site that renders with Sculpin 2 can render with Sculpin 3 out of the box.

For those of you that had to migrate (sometimes painfully) from another platform like Jekyll, I don't want to make you go through that again. At least not with your content. :)

**The goal is for the content of your site to be rendered by Sculpin 3 without additional modification.** The configuration to get your site to render the same way may change, though.

### Sculpin Site Configuration

In general I think that the Sculpin site configuration will not need to change. The `sculpin_site*.yml` files for certain should be able to stay the same. Where things are a little uncertain are with respect to the Kernel configuration.

Whether the Kernel configuration needs to change is up to Symfony 3 and the direction they go with that. I suspect it will not change much but we won't know until we're deep into the migration.

### Sculpin Extensions

Depending on how radically different Symfony 3's Bundle architecture becomes it is possible that existing Sculpin extensions will no longer work in Sculpin 3. If you are building or have worked on Sculpin-specific extensions let me know in the comments so I can get a better idea what kind of impact this will have on the community.

## Sculpin 2 Updates

I'm excited to see these changes roll out throughout the year. However, I want to try and avoid confusion while things will be changing at a fast pace on `master`.

Some of the new features or bug fixes might want to make their way to Sculpin 2. We'll have to take them on a case-by-case basis.

For the foreseeable future Sculpin 2 will be what will be delivered as `sculpin.phar` to new users. When we start building a phar for Sculpin 3 we'll announce how that will work.

In the meantime, we're going to need to update the Sculpin build and deploy process along with the self update functionality so that if you are on Sculpin 2 *you stay on Sculpin 2 when you update*.

We'll provide more news on any gotchas when we have a more concrete plan in place. Until then, know that it is safe to continue to get `sculpin.phar` for the time being and that you won't get any crazy Symfony 3 experimental Sculpin 3 code breaking your site.

---

So, we have a lot of work ahead of us! If all goes as planned we should have a polished Sculpin 3 ready to go by the end of 2015. If you have questions, concerns, or suggestions, leave them in the comments or join us in #sculpin on freenode or Gitter #sculpin to chat with us realtime.
