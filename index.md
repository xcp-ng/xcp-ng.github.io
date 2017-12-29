## What is XCP-ng?

XCP (Xen Cloud Platform) [was the free/libre equivalent of XenServer](https://wiki.xenproject.org/wiki/XCP_Overview) before this last one was open sourced. It was logically shutdown then.

But since [XenServer 7.3 removed a lot of free features](https://xen-orchestra.com/blog/xenserver-7-3/), we need a community solution again: XCP-ng is now the logical successor.

![](https://xen-orchestra.com/blog/content/images/2017/12/xcpng_small.png)

## Who is doing this?

Unlike original XCP, this project is **NOT** backed by Citrix. This is a 100% community project. Current contributors:

* Olivier Lambert (from [Xen Orchestra](https://xen-orchestra.com) project)
* John Else
* Necouchman
* Jon Sands

> Want to join us? Ask!

## What's the goal?

The main goal is to be able to enjoy Xenserver power (XAPI/features) with a real community backed solution (not "one company dependent"). So it should be:
* 99,99% compatible with XenServer (as possible): ie being able to transfer VMs from XS to XCP-ng and vice-versa
* 99,99% compatible with Open Source management solutions (like Xen Orchestra)

## How can I help?

### Direct (technical) help

We need people with experience on these fields:

* centos/RPMs and SRPMs
* XAPI and OCaml
* Deep XenServer knowledge

### Indirect help

Main contributors will be compensated to make the initial build/doc/process working. This cost time and money, contribution will be welcome!

Testing releases will be also a great help.

# Project phases

These are very early/initial estimations. Consider it as more indicative data.

## Phase I: XCP initial prototype

* install from ISO
* working environment without feature restrictions

What's left:

* patch XAPI to remove feature checks
* build XAPI RPM with the patch (using SRPM)
* bundle an ISO with everything (modified XAPI + other modifications to XenServer ISO)

Estimated cost: 6k€ (approx 15 man-day at 400€/day rate)
Estimated release date: Q1 2018

## Phase II: RPM repo and meta package

* update phase I xcp-ng from `yum upgrade`
* turn a CentOS into a XCP-ng ready host

What's left:
`
* create a RPM repo
* create a meta package
* automate the process to put relevent packages there
* avoid conflicts with existing CentOS packages (pinning?)

Estimated cost: between 12k€ and 24k€ (30 to 60 man-day)
Estimated release date: Q2 2018

### Phase III: adding extra stuff

Ideas:

* ZFS driver
* Ceph driver
* Gluster driver
* better compression
* etc.
