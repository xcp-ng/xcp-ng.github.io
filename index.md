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

Some contributors will be compensated to make the initial build/doc/process working. This cost time and money, contribution will be welcome!

Testing the first release will be also a great help.
