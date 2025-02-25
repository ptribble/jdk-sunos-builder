# Building OpenJDK on SunOS

This is the (work in progress) SunOS jdk builder.

The aim is to attempt to download, patch, and build any relevant jdk tag,
and do so for SPARC and x86, and for illumos and Solaris 11.4. It has
currently been tested on current illumos/x86 (specifically Tribblix
m34), and Solaris 11 binary builds are available for
[SPARC](https://pkgs.tribblix.org/openjdk/sparc-solaris/)
up to jdk17, and
[Intel](https://pkgs.tribblix.org/openjdk/intel-solaris/)
up to jdk21. (Those are the latest LTS releases available; later development
builds may also be available.)

It is dependent on the
[jdk-sunos-patches](https://github.com/ptribble/jdk-sunos-patches)
repository, which holds all the patches for each tag.

It should simply be a case of uttering

    ./dobuild jdk17u-jdk-17.0.8-ga

Look in the "jdk-sunos-patches" repository for the list of known versions.

Unless you're developing a new port, or bisecting a bug, generally the
latest version of a given release (which will probably be one of the
update releases, ie jdkXXu) ought to be a good place to start. For
example:

    jdk11u-jdk-11.0.20-ga
    jdk12u-jdk-12.0.2+10
    jdk13u-jdk-13.0.14-ga
    jdk14u-jdk-14.0.2-12

Are all supposed to be supported; later versions need the more extensive
patches available as part of this project.

## Promoting a build

Generally, you need to have a functioning build of one version of the jdk
to build the next version. One point of this project is to allow you to build
the whole chain from source.

Some systems already have the required jdk versions available, in
`/usr/jdk/instances`. Others do not. For those, you'll need to install
a successful build in order to move on. So, the command

    ./dobuild -i jdk12u-jdk-12.0.2+10

will make that version of jdk12 available, ready for the jdk13 build.

To use a Liberica build (which would be a jdk11 release) give the absolute
path to where it was unpacked, for example

    ./dobuild -i /path/to/jdk-11.0.18

## System Setup

First decide on a directory tree where you're going to keep the code and
run the builds. Then set the variables THOME and BUILDROOT in your
environment to point to them, and create them. For example

    THOME=/var/tmp/java
    mkdir -p $THOME
    BUILDROOT=/var/tmp/java-build
    mkdir -p $BUILDROOT

Then checkout the two repositories from github:

    cd $THOME
    git clone https://github.com/ptribble/jdk-sunos-builder
    git clone https://github.com/ptribble/jdk-sunos-patches

You'll also need to install some software in order for the builds to work.

### Tribblix

Install the following overlay:

    zap install-overlay openjdk-build

### Solaris

I'm assuming you're using the Solaris 11 CBE, which already has most of the
development toolchain preinstalled. But you will need:

    pkg install pkg:/developer/gcc-7
    pkg install pkg:/system/font/truetype/dejavu
    pkg install pkg:/developer/versioning/git
    pkg install pkg:/developer/build/autoconf

And you'll need to download a Java 11 JDK to start from - use the
[Liberica JDK](https://bell-sw.com/pages/downloads/#jdk-11-lts).

### Other illumos

On other illumos distributions you'll need to ensure you have a complete
developer toolchain and as many versions of java as are available in that
distribution.

## Documentation

More extensive [documentation](doc/README.md) is available, to help you
through the general porting process.
