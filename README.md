This is the (work in progress) SunOS jdk builder.

The aim is to attempt to download, patch, and build any relevant jdk tag,
and do so for SPARC and x86, and for illumos and Solaris 11.4. It has
currently been spot-tested on current illumos/x86 (specifically Tribblix
m32).

It is dependent on the
[jdk-sunos-patches](https://github.com/ptribble/jdk-sunos-patches)
repository, which holds all the patches for each tag.

It should simply be a case of uttering

    ./dobuild jdk17u-jdk-17.0.8-ga

Look in the "jdk-sunos-patches" repository for the list of known versions.

Unless you're developing a new port, or bisecting a bug, generally the
latest version of a given release (whoich will probably be one of the
update releases, ie jdkXXu) ought to be a good place to start. For
example:

    jdk11u-jdk-11.0.20-ga
    jdk12u-jdk-12.0.2+10
    jdk13u-jdk-13.0.14-ga
    jdk14u-jdk-14.0.2-12

Are all supposed to be supported; later versions need the more extensive
patches available as part of this project.

##System Setup

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

###Tribblix

Install the following overlays:

    zap install-overlay openjdk-build
    zap install-overlay java8
    zap install-overlay java11
    zap install-overlay java17
    zap install openjdk12 openjdk13 openjdk14 openjdk15 openjdk16
    zap install openjdk18 openjdk19 openjdk20 openjdk21

###Solaris

I'm assuming you're using the Solaris 11 CBE, which already has most of the
development toolchain preinstalled. But you will need:

    pkg install pkg:/developer/gcc-7
    pkg install pkg:/system/font/truetype/dejavu
    pkg install pkg:/developer/versioning/git
    pkg install pkg:/developer/build/autoconf

And you'll need to download a Java 11 JDK to start from - use the
[Liberica JDK](https://bell-sw.com/pages/downloads/#jdk-11-lts).

###Other illumos

On other illumos distributions you'll need to ensure you have a complete
developer toolchain and as many versions of java as are available in that
distribution.
