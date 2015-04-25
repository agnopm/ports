# `agnopm` ports

Hi, this repo hosts all of the `agnopm` ports that people have contributed and
that I (greduan) maintain and use myself.

If you have a port you'd like to share, visit the `CONTRIBUTING.md` file first
and then make a pull request. :)

If a new version of software is available but the port is not up-to-date,
contact the maintainer for him to update it or give you maintainer-ship over the
port (if you like).

## Project structure

Ports will reside under their OS's respective folder.  Each port will have its
own folder to host a Pkgfile and patches and stuff.

If a port happens to work perfectly on another OS without any modifications,
then a symlink will be made so as to avoid duplicated effort.

## OS's packages

Preference will *always* be granted to the package available in the OS's
built-in package manager.

Unless the differences are big enough for them to be two different packages, the
`agnopm` port will be deleted if the OS's package manager offers the same
package.

In the case that they are different enough, the `agnopm` port's binaries have to
be renamed so as to not conflict with the OS's binaries.

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
