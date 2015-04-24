# `agnopm` ports

Hey!  If you're reading this you're probably either looking through the ports
to see what kind of stuff is already done, or you're looking for a guide on what
ports are or you're just looking for a reference.

In any case, this repo contains the ports that have been made for the `agno`
package manager.

## Project structure

One of the goals of `agnopm` is to be OS agnostic (assuming your OS is POSIX
compatible).  But not all of the software required to build is POSIX compatible.
For example, there is `make` and `gmake` in OpenBSD, `gmake` being GNU's `make`.
Some software you can't compile without `gmake` but you can with `make`.

The dependencies may be different according to the OS as well.

So what I decided to do was the have the ports reside under different dirs
according to the OS they're tailored for.  But if for whatever reason a port
that was made for another OS works on your OS, then a simple symlink can be
created.

Whenever possible, preference will be granted to the package available in the
OS's built-in package manager.  Which means that if the port becomes available
in the OS's built-in package manager, the port here will be removed.  Unless the
differences are big enough for them to be two different packages.

## Pkgfile format

The general Pkgfile format is borrowed from the [CRUX][c] Linux distro.  This is
because it's a really simple and straightforward format that still manages to
have more than enough features.

[c]: https://crux.nu

However, it's not followed verbatim.  If you're a CRUX user you'll notice the
differences right away most likely.

All Pkgfiles in this repo *will* follow a standard.  Anybody can contribute to
this repo, so established rules are needed.

Visit the `CONTRIBUTING.md` file, found in this very same repo, for the
guidelines and explanation of the format.

You will find a template Pkgfile in this repo (`./Pkgfile`), just to save you
some tedious typing.

## License

All of the ports are under the WTFPL.  There's really no point in putting a more
restrictive license on simple scripts.  However, `agno` itself is under the
ISC license.

    Copyright (c) 2015 Greduan <me@greduan.com>
    This work is free.  You can redistribute it and/or modify it under the
    terms of the Do What The Fuck You Want To Public License, Version 2,
    as published by Sam Hocevar.  See the LICENSE file for more details.
