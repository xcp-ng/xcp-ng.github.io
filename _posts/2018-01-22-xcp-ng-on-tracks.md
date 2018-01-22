---
layout: post
title:  "XCP-ng on tracks"
categories: news
---

We did it! XCP-ng actually works, and this is our first proof-of-concept.

> Note: This is the "report" of *[XCP-ng](http://xcp-ng.github.io/)* project, the fully Open Source build of *XenServer*! The goal will be to deliver turnkey distro (and RPMs repo) to get your turnkey free *XCP-ng* working without any complicated stuff to do.

### XS 7.3 source ISO not yet available

Due to an issue on 7.3 source ISO, we can't use it for now. Citrix is aware of the issue and working on a fix. A fallback on *XenServer* 7.2 was decided instead.

### From 7.2 sources

The initial goal is to make a proof of concept (PoC): we wanted to build a XAPI RPM with feature check removed. And guess what: **we succeeded!**

Let's dig a bit on how to test this by yourself.

> Note: obviously, DO NOT attempt to do this on production machine.

#### Building expendables XenServer VMs

To be able to make experiments, we actually use XenServer on top of… XenServer. That's pretty easy in fact: create a new VM with the `Other Media Install` field and use XS 7.2 ISO to install it.

![xs72install](https://xen-orchestra.com/blog/content/images/2018/01/xs72install.png)

#### Nested

If you want to use a HVM guest on an HVM guest (remember: XenServer on bare-metal, with XenServer in a guest, with on top another guest in HVM), you need to use the experimental nested virtualization mode.

You can enable it easily with `xe`:

```
xe vm-param-set uuid=<VM_UUID> platform:exp-nested-hvm=true
```

You are not ready to make some tests without any risks! Also, don't forget to make a snapshot after the fresh XS 7.2 install, this way you can rollback if needed

## From SRPM to RPM

The process is relatively easy to understand:

1. XAPI SRPM package was downloaded (from [7.2 source ISO](http://downloadns.citrix.com.edgesuite.net/12645/XenServer-7.2.0-source.iso))
2. We added a patch to remove feature check
3. The package was rebuild with the patch

We got a nice and brand new XAPI RPM package, `xapi-core-1.30.0-1.x86_64.rpm`

Now, we are ready to test it :)

## Deploy on your test host

Let's install it into the host. But before, let's do a simple check: installing a HVM guest with CentOS + xen tools.

![centosnested](https://xen-orchestra.com/blog/content/images/2018/01/centosnested.png)

Now, we'll have max vCPU number at 2 and current vCPU number at 1.

![vmlimits](https://xen-orchestra.com/blog/content/images/2018/01/vmlimits.png)

If we try to add vCPUs in live, we got:

```
# xe vm-vcpu-hotplug new-vcpus=2 uuid=<VM_UUID> 
This operation is not allowed because your license lacks a needed feature.  Please contact your support representative.
feature: Live_set_vcpus

```

Okay, let's install manually the RPM now:

```
# rpm -U xapi-core-1.30.0-1.x86_64.rpm --force
```

And restart the toolstack:

```
# xe-toolstack-restart
```

Let's do the test again:

```
# xe vm-vcpu-hotplug new-vcpus=2 uuid=<VM_UUID>
```

**This time, it worked!** The VM was able to get VCPUs changed in live (like back in 7.0 before Citrix decided to remove this feature from Free edition).

## RPM repo

Now, we'll try to have a *XCP-ng* distro, embedding the right version of XAPI directly. This will allow to upgrade *XenServer* to *XCP-ng* (similar to a 7.1 -> 7.2 upgrade).

But we also want to explore the "RPM way", ie adding a RPM repo into your existing XS, then `yum upgrade` to transform it into a XCP-ng ready host. **In fact, it's already working!**

Take a clean **7.2** host (again, a test one!), and add this in the new file `/etc/yum.repos.d/xcp-ng.repo`:

```
[xcpng]
name=Test XCP-ng with 7.2
baseurl=http://updates.xcp-ng.org/7.2/
enabled=1
gpgcheck=0
```

The original XAPI will be replaced by the modified one:

```
yum reinstall xapi-core
```

Then do a `xe-restart-toolstack` to get actually rid of license checks. 

But you can also get **all the 7.2 updates** (including Meltdown patch!) without install packs anymore, just with a `yum upgrade`! Because we filled the repo with the RPMs that are in fact in the update packs themselves. This is the direction we want to go, as as soon 7.3 source ISO is available, we'll be able to make it real.

## What's next?

XCP-ng project will have a new dedicated home with a blog too. Again, don't forget to [register here](https://mailchi.mp/3bc90e48d2f7/xcp-ng) to get latest news about XCP-ng project into your inbox!

[![xcpng400](https://xen-orchestra.com/blog/content/images/2018/01/xcpng400.png)](https://mailchi.mp/3bc90e48d2f7/xcp-ng)