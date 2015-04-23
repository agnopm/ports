# Contributing to `agnopm`'s ports repo

In this file we will go over the guidelines of making a port and go over a brief
tutorial of the format the Pkgfiles will have.  More than guidelines these are
rules however, but still guidelines.

## Header

Every `agno` port has a header.  This header contains meta info that is of no
interest to `agno`, but it is for the porter.  It goes like so:

``` sh
# Description:  Short description of software
# URL:          http://softwares.website.url/goes/here
# Maintainer:   Some Guy <his@email.com>
# Packager:     Some Guy <his@email.com>
# OS Depends:   comma, separated, list, of, deps
# agno Depends: comma, separated, list, of, deps
```

In that order.  Not one above the other or something and none are omitted no
matter the case.  They must also be aligned, for readability's sake.

### Description

This is pretty self explanatory.  Try to keep your description under 80
characters if it's possible, as in the description line shouldn't be longer than
80 characters.  And whenever possible use the short description that the
software is using, unless it's ridiculously long or it doesn't have one.

### URL

Again, pretty self explanatory.  Just go to the software's website (even if it's
GitHub) and just copy the URL and paste it here.

If the software doesn't have a "website", so to speak, then just paste the URL
of where one can find the source code.

### Maintainer and Packager

These two are related but not the same.  The maintainer is he (or she) who is
keeping up with updates and keeping the port up-to-date.  The packager is
whoever originally made the port.

Both of these are to remain present, even if they are both the same.

The format goes "First name Last name <some at email dot com>".  If you are
uncomfortable with sharing your first and last name you can use your username.
But no mixing of real name and username, and it can't be only first name or only
last name.

### OS Depends and agno Depends

`OS Depends` and `agno Depends` both tell the user what this piece of software
needs in order to be built or to run correctly.  Dependencies are comma
separated (for readability).  If there are no dependencies then they can just be
left empty (or one of them empty) etc.

`OS Depends` is talking specifically about what the OS's package manager has
available.

`agno Depends` is talking about dependencies that can't be satisfied by the OS's
package manager, thus they are available as an `agno` port.

## Variables

These variables give important info to the package manager about what port it is
working with and also allow it to do some work for you.

``` sh
name=the_silver_searcher
version=0.29.1
release=1
source="https://github.com/ggreer/the_silver_searcher/archive/${version}.tar.gz"
```

### `name`

This is pretty simple.  You shouldn't use any spaces in the port's name, if you
require a space, whatever the reason may be, just use a dash (`-`) instead.  If
you're not sure what to name it, take a look at what the same package has been
named in [Arch Linux][al].

[al]: https://www.archlinux.org

### `version`

Another straight forward one, make it the same as the software version you are
going to install.

If you are pulling the latest commit from Git to get your source, you can put
`git` as the version.  If you are pulling from Git but using a tag or a commit
hash to pull out a specific version of the software, use the version you are
using as the `version` string.

### `release`

This usually stays at `1`, but this tells you what version of the current
software version you are packaging.

That is to say, if you make a port for version `0.2.2` and you push it,
`release` will be `1`, but if you later make a change to the port but the
version is still `0.2.2`, then `release` will now be `2`.

### `source`

This variable defines the files that will be necessary for you to build your
port.  This is a *string*, not a Bash array, this is for POSIX compatibility.
Sources are separated by a space

More often than not you'll use the `version` variable in the URL string so as to
not have to type it out every time.  Using the `name` variable is not
recommended, as some software don't use the package name in the URL, also it
makes the url dirtier.

Variables used inside the string should be enclosed around `${}` for clarity and
safety.  Do not use `$var` use `${var}`.

## Build process

The build process is arguably the most important part of the port.  This is the
body of the port.  It defines what will be done to build the package and to
install it.  It would look something like this (commented for your convenience):

``` sh
agno_build() {
	# when this is run you are dropped in the same dir with your downloaded files so
	# here we're just cd'ing into the dir wit the source
	cd $name-$version

	# buildin
	./build.sh
	# prefix should _always_ be /usr and the mandir should be /usr/man
	./configure --prefix=/usr \
		--mandir=/usr/man
}

agno_install() {
	# otherwise we're in the WORK dir, not in the package's source code dir
	cd $name-$version
	# installing, DESTDIR is conveniently labeled AGNO_DESTDIR :)
	make DESTDIR=$AGNO_DESTDIR install
}
```

Please note that you should use exactly one tab, a real tab, not four or eight
spaces or whatever.  You should only indent the body of the `agno_build()` and
`agno_install()` functions.

### `agno_build()`

This function is just a normal shell function, called by `agnomk` when it is
ready to build your port.  What goes on inside it is only what you write inside
of it.  Only build procedures should be in here.

### `agno_install()`

Same as `agno_build()`, except this function should only do installing
procedures.

The reason these two functions are separated, unlike CRUX's Pkgfiles is for
possible future expansion where this may be necessary, and we don't want to be
updating all the ports when that happens and we only had one function.  :)
