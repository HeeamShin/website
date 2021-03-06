---
title: webOS OSE 1.10.0 Release
date: 2019-07-30
slug: webos-ose-1-10-0-release
posttype: release
toc: false
---

We are pleased to announce the new release of webOS Open Source Edition (OSE)!

This release brings you several new features and important changes. Highlights include:

  - [VirtualBox Emulator](#virtualbox-emulator)
  - [resize-rootfs](#resize-rootfs)
  - [Library update and issue fixes](#library-update-and-issue-fixes)

## VirtualBox Emulator

From this release, webOS OSE provides an emulator that runs as a virtual machine on [Oracle VM VirtualBox](https://www.virtualbox.org/).

In contrast with the previous QEMUx86 emulator that supported Ubuntu Linux only, the VirtualBox-based emulator supports widely used host operating systems --- Ubuntu Linux, macOS, and Windows. With the new emulator, developers using different host systems can experience implementing and testing apps for webOS OSE. For more information on how to set up and use the emulator, check the [VirtualBox Emulator User Guide]({{< relref "emulator-user-guide" >}}).

{{< note >}}
The QEMUx86 emulator for Linux is no longer actively maintained, so we strongly recommend that you use VirtualBox-based emulator instead.
{{< /note >}}

## resize-rootfs

Due to change of rootfs, a script called **resize-rootfs** has been introduced from this release.

resize-rootfs is a script to increase rootfs partition in order to use the full microSD card storage. Note that resize-rootfs works only for the Raspberry Pi target and is executed only once at the very first boot.

Here's an overview of how resize-rootfs works.

1.  Rewrite the partition table by using `fdisk`
      - At this step, resize-rootfs increases partition 2 endpoint to the last block of a microSD card.
2.  Resize rootfs by using `resize2fs`
      - The `resize2fs` will be run as online resizing mode.
3.  At the last stage, touch `/var/luna/preferences/rootfs_resized`
      - This operation is performed in order to prevent duplicated execution.

{{< note >}}
To block resize-rootfs for some reason (e.g. to create your own partition), you need to create `{second partition of microSD}/var/luna/preferences/rootfs_resized` immediately after you flash the image to the microSD card.
{{< /note >}}

## Library Update and Issue Fixes

This release includes the following library update.

  - Upgraded the curl version from 7.63.0 to 7.64.1. For details, see the [curl-library release notes](https://curl.haxx.se/mail/lib-2019-03/0126.html).

In addition, the following issues have been resolved with this release.

  - The Bluetooth device discovery issue, which was caused by BlueZ upgrade to 5.50 in accordance with the Yocto upgrade, has been resolved.
  - The crash issue of Camera service and g-camera-pipeline that appeared after Yocto upgrade has been fixed.
