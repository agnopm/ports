# `agnopm` ports

Hi, this repo hosts all of the `agnopm` ports that people have contributed and
that I (@greduan) maintain myself.  If you have a port you'd like to share,
visit the `CONTRIBUTING.md` file first and then make a pull request. :)

## Project structure

One of the goals of `agnopm` is to be OS agnostic (assuming your OS is POSIX
compatible).  But not all the OSs have the same software or libraries available
to them.

For example, there is `make` and `gmake` in OpenBSD, `gmake` being GNU's `make`.
Some software you can't compile without `gmake` but you can with `make`.  So
OpenBSD ports need to know when to use `make` and when to use `gmake`.

So what I decided to do was the have the ports reside under different dirs
according to the OS they're tailored for.  If for whatever reason a port that
was made for another OS works on your OS, then a simple symlink can be created,
this is especially useful if the software has no particular dependencies.

Ports will reside under

## OS's packages

Preference will *always* be granted to the package available in the OS's
built-in package manager.  Which means that if the port becomes available
in the OS's built-in package manager, the port here will be removed.  Unless the
differences are big enough for them to be two different packages, but in that
case the `agnopm` port's binaries have to be renamed so as to not conflict with
the OS's binaries.

## Pkgfile format

All Pkgfiles in this repo *will* follow a standard.  Anybody can contribute to
this repo, so established rules are needed.

Visit the `CONTRIBUTING.md` file, found in this same repo, for the guidelines
and explanation of the format.

You will find a template Pkgfile in this repo as well (`./Pkgfile`), just to
save you some tedious typing.

## License

All of the ports are under the WTFPL.  There's really no point or benefit in
putting a more restrictive license on these ports.  However, `agno` is under the
ISC license.

    Copyright (c) 2015 Greduan <me@greduan.com>
    This work is free.  You can redistribute it and/or modify it under the
    terms of the Do What The Fuck You Want To Public License, Version 2,
    as published by Sam Hocevar.  See the LICENSE file for more details.
