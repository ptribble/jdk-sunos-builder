# How the patches are structured

The way the patches are structured is, frankly, a bit of a mess. Mostly
this is historical evolution.

There are essentially 4 types of patches:

* The gcc port. These are present in all the releases, so you'll see them
all the way back to JDK8.

* The main removal patch, called java-solaris-sparc.patch. This was
originally the patch for the commit that removed SPARC and Solaris support.
As a result, it's reversed and needs to be applied with -R.

* Ongoing illumos/Solaris/SPARC support patches, which have been created
to match the ongoing changes to the JDK.

* The patches to enable a port to zero (an alternate JVM)

What this means is that in some cases the third class of patches actually
patches things that were patched by earlier patches. More recently I've
tried to avoid that to keep the patching simple.

The SPARC restoration is a little cleaner. I've removed all of that from
java-solaris-sparc.patch and added the SPARC patches separately.

## Cleanliness

The aim (now) is that the patches apply with zero noise. This means no
fuzz and no line number offsets. This generally makes everything clean,
ensures that no .orig files clutter up the source tree, and also gives
a hint of what files have been changed and might need looking at, because
then you'll see new patch noise.
