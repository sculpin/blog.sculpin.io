---
title: "Sculpin is now in nixpkgs"
author:
  shortname: "opdavies"
  name: "Oliver Davies"
---

[nixpkgs](https://search.nixos.org/packages) is the [largest online package repository](https://repology.org/repositories/statistics/total) with more than 140,000 packages, and now Sculpin is one of them because Sculpin 3.3.1 [has been merged](https://github.com/NixOS/nixpkgs/pull/476433) into nixpkgs-unstable!

Now, if you use the `nix` command line tool or the NixOS operating system, you can easily create a new shell with Sculpin installed by running this one command:

    nix shell "github:NixOS/nixpkgs/nixpkgs-unstable#sculpin"

No need to have PHP or Composer installed separately.

Within the shell, run your `sculpin` commands normally.

When finished, exit the shell and Sculpin will be gone until you need it again.

Or, run an ad-hoc command directly:

    nix run "github:NixOS/nixpkgs/nixpkgs-unstable#sculpin" generate -- --server --watch

This is how I'm running this website to write this post. :)

In both cases, Nix will download and install all of the dependencies for you, so Sculpin just works.

## What about flakes?

For an example using a flake, see my [nix-sculpin-template](https://git.oliverdavies.uk/opdavies/nix-sculpin-template).

## What about bundles?

If you use bundles in your Sculpin site, you can create your own `autoload.php` file and wrap Sculpin to use it.

See [my website repository](https://git.oliverdavies.uk/opdavies/oliverdavies.uk/src/branch/main/www.oliverdavies.uk) for an example.

## Want to learn more about Nix?

Check out <https://nixos.org> or [my "Nix for Developers" talk](https://www.oliverdavies.uk/presentations/nix-developers).

---

As a long-time Sculpin user, it's great to see it in nixpkgs and bring together two of my favourite open source projects.
