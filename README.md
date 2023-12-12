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
