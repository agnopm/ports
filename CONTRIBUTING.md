# Contributing to `agnopm`'s ports repo

In this file we will go over the guidelines of making a port and go over a brief
tutorial of the format the Pkgfiles will have.  More than guidelines these are
rules however, but still guidelines.

A port is divided into 3 sections:

- **Header** - General info for the user
- **Variables** - Information about the package that `agno` needs to work
- **Functions** - What runs your building and installing proceduers

Throughout this document I'll be using the [port for abduco(1)][ab] as an
example.

[ap]: https://github.com/agnopm/ports/blob/master/openbsd/abduco/Pkgfile

## Header

Every `agnopm` port has a header.  This header contains meta info that is of no
interest to `agno`, but it is of interest for the users.  It goes like so:

``` sh
# Description:  Session management in a clean and simple way
# URL:          http://brain-dump.org/projects/abduco
# Maintainer:   Eduardo Lavaque, me at greduan dot com
# Packager:     Eduardo Lavaque, me at greduan dot com
# OS Depends:
# agno Depends:
```

In that order.  Not one above the other or something and none are omitted no
matter the case.  They must be aligned to "agno Depends", for readability's
sake.

### Description

The description is a short one-liner that should make it clear to the user this
is the piece of software that he's looking for.

The description line shouldn't be longer than 80 characters.  And whenever
possible use the short description that the software offers in its homepage,
unless it's ridiculously long or it doesn't have one.

If pulling from Git, "(Git checkout)" should be added to the end of the
description.

### URL

This should just let the user know where he can find the software's homepage.

Just go to the software's website and just copy the URL and paste it here.

If the software doesn't have a "website", so to speak, then just paste the URL
of where one can find the source code, e.g. GitHub or cgit.

### Maintainer and Packager

Just to let the user know who to contact in case he wants to submit a bug, make
a feature request of the port or something similar.

These two are related but not the same.  The maintainer is he (or she) who is
keeping up with the software's updates and keeping the port up-to-date
accordingly.  The packager is whoever originally wrote the port.

Both of these are to remain present, for proper credit, even if they are both
the same and the maintainer should be above of the packager, as he is a more
relevant terminal to contact.

The format goes "Firstname Lastname, some at email dot com".  If you are
uncomfortable with sharing your first and last name you can use your username.
But no mixing of real name and username, and it can't be only first name or only
last name, to avoid confusion on if it's your username or not.

### OS Depends and agno Depends

"OS Depends" and "agno Depends" both tell the user what this piece of software
needs in order to be built or to run correctly.

Dependencies are space separated (for scriptability).  If there are no
dependencies then they can just be left empty (or one of them empty) etc.

"OS Depends" is talking specifically about what the OS's package manager has
available.  This one is above "agno Depends" because of the preference of OS
native packages.

"agno Depends" is talking about dependencies that can't be satisfied by the OS's
package manager, thus they are available as an `agnopm` port.

## Variables

These variables give important info to the package manager about what port it is
working with and also allow it to do some work for you.

``` sh
name=abduco
version=0.4
release=1
source="http://brain-dump.org/projects/abduco/abduco-${version}.tar.gz
bsd.patch"
```

### `name`

This is a unique identifier for each port.  Trouble will happen if it's not
unique.

You shouldn't use any spaces in the port's name, if you require a space,
whatever the reason may be, just use a dash (`-`) instead.  If you're not sure
what to name it, take a look at what the same package has been named in [Arch
Linux][al].

[al]: https://www.archlinux.org

Incidentally, the folder which contains the Pkgfile should have the same name as
the `name` variable.

### `version`

This should be the version number of the software the port installs.

If you are pulling the latest commit from Git to get your source, you can put
`git` as the version.  If you are pulling from Git but using a tag or a commit
hash to pull out a specific version of the software, use the version you are
checking out as the `version` number.  Remember to add `git` to the list of "OS
Depends".

### `release`

This is the port's version, not the software's version.  This tends to stay at
`1`.

For example: If you make a port with version `0.2.2` and you push it, `release`
will be `1`, but if you later make a change to the port but the version is still
`0.2.2`, then `release` will now be `2`.

### `source`

This variable defines the files that will be necessary for you to build your
port.  Any file not defined here will *not* be available for you to use in the
`$AGNO_WORK` dir.

This is should be a *string*, not a Bash array, this is for POSIX compatibility.
Sources can be separated by a space or a newline, but for readability a newline
is preferred.

Variables used inside the string should be enclosed around `${}` for clarity and
safety, i.e. do not use `$var`, use `${var}`.

The sources that `agno` supports at the moment are:

- `http(s)://` - It supports HTTP and HTTPS protocols (through `curl(1)`).
- `ftp(s)://` - It supports FTP and FTPS protocols (through `curl(1)`).
- `git://` - It supports the Git protocol.  Will be cloned as `$name-git`.
- file - Anything that isn't one of the above, e.g. `bsd.patch`. The file will
  be searched for in the same dir in which the Pkgfile is in.

## Functions

The functions define what will be done to build the package and to install it.
These are just plain old shell script functions.  It would look something like
this (couple comments for your understanding):

``` sh
agno_build() {
	# otherwise you'd be in $AGNO_WORK
	cd $name-$version

	patch -i $AGNO_WORK/bsd.patch

	make
}

agno_install() {
	# otherwise you'd be in $AGNO_WORK
	cd $name-$version

	make DESTDIR=$AGNO_DESTDIR PREFIX=/usr MANPREFIX=/usr/man install
}
```

Note that you should use exactly one tab, a real tab, not four or eight spaces
or whatever.  Only the insides of the `agno_install()` and `agno_build()`
functions should be indented, nothing else in the file should contain tabs.

It is important to note, before calling either of these functions the directory
is changed to `$AGNO_WORK`, this is for consistency.

The reason these two functions are separated, unlike CRUX's Pkgfiles is for
possible future expansion where this may be necessary, and we don't want to be
updating all the ports when that happens because we only had one function. :)

### `agno_build()`

Called by `agnomk` when it is ready to build your port.  What goes on inside it
is only what you write inside of it, so it could potentially be empty if you are
downloading a binary or installing a font or something like that.

### `agno_install()`

Called by `agnomk` when it is ready to see how your port would install.  What
goes on inside it is only what you write inside of it, while this could
potentially be empty, that would render your port effectively useless so it is
not recommended.
