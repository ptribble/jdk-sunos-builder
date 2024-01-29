# Running the dobuild script

The dobuild script is supposed to be reasonably straightforward. A
simple

    ./dobuild jdk17u-jdk-17.0.8-ga

will download, patch, and build the relevant tag.

There are several flags you can use.

With -d, just download the given tag.

With -p, download if necessary, and apply patches.

With -b, download if necessary, apply patches, and run a build.

So, -b is the normal operation.

The variants -P and -B will delete an existing unpacked copy and start
afresh.

In practice, what you'll want to do in development is use -p to check
if any new patches apply cleanly, repeat with -P as you develop changes
to the patches, then once you're happy do the build step.

## Using a build to compile another

One part of the process is that you eventually need to use one version of
the JDK in order to build the next. If it finds an installed version it
will use that, but if you're building the whole chain from scratch you
won't have that. So you can use the -i flag, for example

    ./dobuild -i jdk12u-jdk-12.0.2+10

will make that version of jdk12 available, ready for the jdk13 build.

## Exporting a build

The build process will generate a fully deployable image of the jdk, but it
will be embedded in the build directory. The -i flag above knows where to
find the image for use within another build, but if you want to deploy the
build somewhere else then you'll need a standalone copy.

You can use the -e flag for this

    ./dobuild -e jdk-jdk-16-24

will generate a tarball called jdk-jdk-16-24.tar.gz that will unpack into a
directory jdk-jdk-16-24, and will tell you where it's put it.
