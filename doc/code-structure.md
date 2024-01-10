# The code layout

In current releases, you'll largely be interested in 2 parts of the source
tree.

(In the older days of the mercurial forest the code was laid out quite
differently.)

## make

This is where the various makefiles live. This doesn't change all that much,
but we have to patch the makefiles to add solaris support back (generally,
we have slightly different flags)

## src

The main area is src/hotspot, which is where most of the platform and
architecture specific code resides. There's code for a particular
operating system (os), code for a particular processor (cpu), and for
an operating system running on a give processor (os_cpu). So we're
interested in:

* os/solaris
* cpu/sparc
* os_cpu/solaris_x86
* os_cpu/solaris_sparc

We don't need to worry about os/x86, because that's already present and
supported.

There's also os/posix, which provides a lot of shared code, avoiding the
need for duplicate implementations. There has been a lot of effort to
remove the per-os implementations into posix, which makes life much
easier. (One reason there were different implementations was that each
operating system originally supported was dramatically different. In
2024 that's not really the case, and everything is close enough to posix
that the code would be essentially the same. In the solaris port we do have
a number  of specific implementations, but it's not entirely clear if
they're still necessary - many were due to oddities from decades ago.)
