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

In practice, what you'll want to do in development is use -p to check
if any new patches apply cleanly, then once you're happy do the build
step.

## Using a build to compile another

One part of the process is that you eventually need to use one version of
the JDK in order to build the next. If it finds an installed version it
will use that, but if you're building the whole chain from scratch you
won't have that. So you can use the -i flag, for example

    ./dobuild -i jdk12u-jdk-12.0.2+10

will make that version of jdk12 available, ready for the jdk13 build.
