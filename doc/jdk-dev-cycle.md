# The JDK development cycle

JDK is developed on trunk. That's the main jdk development repo.

Releases are made every 6 months. The majority are intermediate
releases, while some are classed as LTS (Long-Term Support). The LTS
releases are JDK8, JDK11, JDK17, and JDK21. Originally in the new
scheme it was intended to promote every 6th release to LTS (hence
the gap between JDK11 and JDK17) but that was felt to be too long, so
the current aim is every fourth release (so every 2 years).

## The cycle of a release

* JDK XX is developed in the main jdk repository for 6 months, with
a build tag published every week.

* After 6 months, a stabilisation repo, jdkxx, is created. The main
repository then continues with development of JDK xx+1.

* Once released (typically another 3 months) the jdkxx repository is
frozen and and updates repository jdkxxu is created.

You can see this in the naming of the patches. Take jdk16 as an example -
the tags from the main repository are named jdk-jdk-16-14 - the first
component is the repository, the second is always "jdk" as the name of
the project, the third is the version, the last is the build. So you'll
see up to build 26 or 27 (for the 6 month cycle, builds every week). Then
it switches to the tag being jdk16-jdk-16-36 from the jdk16 stabilisation
repository. Typically the last build (the one for GA) is about 35 or 36.
And then you get jdk16u-jdk-16.0.2-7 which is from the jdk16u repository,
update 2, build 7.

For most releases, you probably get 2 updates. The update cycle matches
Oracle's quarterly CPU (Critical Patch Update) cycle. And those 2 quarterly
updates tide you over the 6 months until the next release.

Some of the older releases (13 and 15) were supported for longer, as it was
a long time before the next LTS was due.

The update releases tend not to be managed by Oracle, generally Red Hat
and sometime Azul look after those.

## Within a cycle

Activity varies within a cycle. Clearly within the stabilisation repository
you should see only bugfixes. There will be no new features and very little
churn.

Things are quiet at the start of a cycle. Imagine that everyone's taking
a breather after the release.

So most of the churn in terms of new features and big changes occurs at
around the build 20 mark.

## Plus or minus?

In the current github world, the tag will be xx-yy (that's what the tarball
you download will be named and unpack to), but the actual tag will be xx+yy.

Originally in mercurial both were xx+yy. Some of the older patches were
written for mercurial, and have been switched to the xx-yy convention and
the downloads come from github.
