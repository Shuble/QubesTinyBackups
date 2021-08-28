# QubesTinyBackups
Application for Qubes for the generation, distribution, testing, and usage of tiny backups.

## Introduction

Everyone knows that creating regular backups for your systems is an absolute necessity, and that you should create 
multiple backups stored in multiple locations. The issue is that for many people, the size of their systems makes
this task a chore if not prohibitively expensive. If done at all, in many cases it will be to one or two large
external disks at a person's home or office.

Things are a bit better nowadays with the prevelancy of cheap cloud storage, making it feasible for many to
perform regular remote backups. Incremental backups mitigate the networking issues associated with moving a large
amount of data to a remote location. But again there's still at least some cost associated with renting cloud
storage, making it difficult to add redundancy by using multiple vendors or physical drives, and while
incremental backups allow you to backup a large system regularly without using much bandwidth, the fact remains
that in order to do a full restore of your system, you must download the entire thing.

This last point is important, a backup strategy is useless unless it is rigorously tested on a regular basis. If
actually using backups is a pain, then they're less likely to be tested, and when the time comes to actually use
them, on top of the pain that was already known, comes the additional pain of all the problems that were 
unknown. Any complexity added on top of this, such as encryption, deduplication, compression, etc., only make
this problem worse.

## Tiny backups

The solution is to understand that for the vast majority of people, the majority of the space taken up on their
systems comes from **downloaded applications, packages, and tools**. The amount of actually unique and personal
data is relatively tiny. Thus a backup containing this personal data and a note of what's been downloaded is
in many cases just as good as a backup of the entire system.

## Tiny backups for Qubes

Qubes OS already takes advantage of this phenomenon, many App VMs can be made from a single Template VM without
taking up much space, because for an App VM everything outside of the Home directory is shared with the
template, and any modifications to this area are thrown away when the App VM is shut down.

The native backup tool for Qubes takes this into account, it only backs up the home directory of App VMs, but
for template VMs it still takes the approach of performing a backup of the entire system. It is also limited
in its functionality, it offers built in compression and encryption, but some may wish for more advanced
capabilities such as deduplication, or the ability to integrate with cloud storage.

QubesTinyBackups is meant to provided this additional functionality.

## Dom0 concerns

It is a bad idea to download anything to Dom0, if you use Qubes you likely already understand this fact. If a
hacker can gain access to dom0, then he effectively owns the entire system. I've been looking into ways to
minimize QubesTinyBackups dom0 usage, but currently it is needed to kick off backups and to transfer data
between Qubes.
