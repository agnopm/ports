# `agnopm` ports

Hi, this repo hosts all of the `agnopm` ports that people have contributed and
that I (greduan) maintain and use myself.

If you have a port you'd like to share, visit the `CONTRIBUTING.md` file first
and then make a pull request. :)

If a new version of software is available but the port is not up-to-date,
contact the maintainer for him to update it or give you maintainer-ship over the
port (if you both agree).

## Project structure

Ports will reside under their OS's respective folder.  Each port will have its
own folder to host a Pkgfile and patches and stuff.

If a port happens to work perfectly on another OS without any modifications,
then a symlink will be made so as to avoid duplicated effort.

## OS's packages

Depending on the kind of package, preference may be granted to the OS's or to
`agnopm`'s package.

For example, with libraries it is generally preferred to use the OS's version,
because a new library version overriding the default OS's version may break some
or many applications.  This of course is not something to worry about if the
port offers a library not made available by the OS's package manager.

But for applications, binaries, that sort of thing, one may prefer to use
`agnopm`'s packages as they are more up-to-date, especially if one is using a
stable OS, e.g. Debian or OpenBSD, whose's applications only change after the
upgrade or very very slowly (unless one is following a more up-to-date branch).

## Pkgfile format

All Pkgfiles in this repo *will* follow a standard.  Anybody can contribute to
this repo so established rules are needed.

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
