# The porting process

As described in the jdk development cycle, a new tag is published every
week. What I do is try and build every tag, so that the scale of changes
is kept small, and you can see what changed.

## Try patching

I apply the patches from the previous tag, and look for noise. If there
are failures, you need to fix them. Any other patch noise is investigated,
as it indicates the file being patched has been modified. The patches
are updated if necessary so that they apply without noise.

## Try a build

One the patching is clean, try a build.

## Fix any failures

If the build fails, any failures need to be fixed. This is where things
get interesting.

The general approach if something breaks is to look at another platform
(or architecture) to see what's changed between this tag and the previous
successful one. If you get a compilation failure you can see which area (ie
whether it's in os, cpu, or os_cpu) appears affected. Then look at maybe
linux or aix to see what's changed there.

A lot of the changes I've seen are simple method renaming or signature
changes. In some cases where a new method is added, all you need to do
is provide a stub. If a common method is removed, then check to see if it's
in use anywhere. If it's not it can just be removed; if it's used locally
then maybe you just just move the scope to be local (or os::Solaris).
