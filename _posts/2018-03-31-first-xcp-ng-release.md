---
layout: post
title:  "First XCP-ng release"
categories: news
comments: true
---

We said "the first XCP-ng release will be available in Q1". Guess what? **We did it**.

> Mirror, mirror, where's your fastest server? We need your help to host this ISO everywhere in the world to get better download speed. If you can provide a mirror, please let us know where (link and hosting country) on [Twitter](https://twitter.com/xcpng), IRC (#xcp-ng on Freenode) or in the comment section. We'll add it here then.

[Download XCP-ng ISO here](http://xcp-ng.org/7.4/XCP-ng_7.4.iso).

> Md5sum: `ea2a9b90218537b546d1f399ae2ace95`

> What about pro support? A recurrent question from various companies is support related. Good news: in a near future, **XCP-ng will be backed with professional support**, based on the fully Open Source version, **without any feature restrictions**. We also aim to put XCP-ng in an Open Source foundation as soon as we can, to be certain to be available to **everyone** without limits.

## A first test release

XCP-ng is **based on XenServer 7.4**. Remember this first release is a go for testing and gathering your feedback. There is still some stuff to improve, like:

* including our RPM repos
* doing more test (that's also up to you!)
* improve compatibility (read more on a paragaph below)
* doing a real build process

**Keep that in mind before doing anything with production systems**. This is **only the first release** and it means you can either **test it or wait** for more feedback.

> It's possible that next improved release will require a full "upgrade" (ie like reinstall while saving your existing VMs on it, like a traditional XenServer upgrade). We can't know for sure right now.

![](/assets/images/xcpngstick1.jpg)

## What's in it?

With the ISO we provided:

* You can install XCP-ng from scratch on your hardware
* You can upgrade an existing XenServer to XCP-ng
* You can enjoy **ALL** features without restrictions

> Note: XenServer ISO is detecting XCP-ng install and should be able to "downgrade" it (ie: getting back to XenServer). However, this is not tested.

### Compatibility

**Please read this before installing it**

Due to change in the product name (ie XCP-ng vs XenServer), some operations could fail:

* migrating a VM from XenServer **to** XCP-ng will work, **NOT** the opposite for now
* Recent version of XenCenter fails to connect (but XO works perfectly!)

> If you want a quick UI to manage your XCP-ng, you can deploy Xen Orchestra by just typing `bash -c "$(curl -s http://xoa.io/deploy)"` inside your XCP-ng console. This will deploy a VM with a web UI.


> Note: Xen Orchestra is **100% compatible with XCP-ng**. You can either deploy the free turnkey appliance or install it from the sources yourself. If you already use it, just add the host in Settings/server, like any other XenServer host:

![](/assets/images/connectxo.png)

## Install procedure

It's very similar to XenServer install. First, [download our ISO here]().

Then, install from USB key, eg with `dd if=XCP-ng_7.4.iso of=/dev/sdX bs=8M status=progress oflag=direct`. You can also burn a real CD or use a Windows program to create bootable USB key from an ISO file.

Finally, it's pretty straightforward:

![](/assets/images/xcpinstall/install1.png)

![](/assets/images/xcpinstall/install2.png)

![](/assets/images/xcpinstall/install3.png)

![](/assets/images/xcpinstall/install4.png)

![](/assets/images/xcpinstall/install5.png)

![](/assets/images/xcpinstall/install6.png)

![](/assets/images/xcpinstall/install7.png)

That's it!

![](/assets/images/xcpinstall/install8.png)

Now it will boot:

![](/assets/images/xcpinstall/boot1.png)

![](/assets/images/xcpinstall/boot2.png)

And you're in:

![](/assets/images/xcpinstall/boot3.png)
 
## What's next?

We'd like to improve compatibility, add a default repo for next updates/patches and obviously improve our build process (that wasn't merely a process for now, but more a pile of various manual stuff). The build process is vital to keep up the pace and then later including extra features!

> Stay tuned on all our coming news by registering here! We also have a [Twitter account](https://twitter.com/xcpng).

## Sponsors

We'd like to thanks again all our invididual backers, but also all the sponsors. There is now a dedicated page listed there: https://xcp-ng.github.io/sponsors