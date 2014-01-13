ocz-revodrive-2.6-proxmox
=========================

Support for OCZ RevoDrive3, RevoDrive3 X2, zDrive R4 in Proxmox is possible. This repository contains all the information needed to patch your kernel and backport RevoDrive support in the stable 2.6.32 Proxmox kernel (The only one with OpenVZ support at the time of writing, Gen 2014).

## Creating a patch

diff -Naur linux-source-2.6.32-openvz-042stab084.14-amd64 linux-source-2.6.32-openvz-042stab084.14-amd64-ocz > ocz.patch

## The original request

This patch request uis the first one on the proxmox/pve-kernel-2.6.32 repository! You can read the original message on https://github.com/proxmox/pve-kernel-2.6.32/issues/1 or below.

Dear Proxmox kernel mantainers,

OCZ is providing a terrible Linux support, in an attempt to "protect" the technology of their VCA chip, build on a Marvell 88SE9485 controller. Basically they try to push down the adoption of RevoDrive3 and RevoDrive3 X2 on Linux machines in favor of other "enterprise" class products (zDrive R4). All summed, this attitude will grant lifetime exclusion from the kernel and painful user experience.

In reality the device just works with minor modifications of the mvsas driver [1]. Modifications that are already included in the mainline 3.2 kernel [2].

Additionally it seems, according to the report of b3rlin3r, that VCA actually decrease performance compared to the standard Marvell device [4]. Vanilla mvsas driver does 4612 TPs VS 3605 TPs for the OCZ VCA driver (actually 2, oczpcie and oczvca).

My request is to backport the robbat2 patch to the rhel6-2.6.32 [3] kernel, it's just a matter of adding some PCI ids to the driver.

Thanks and have a great day,
Francesco ascii Ongaro
http://www.ush.it/ - http://www.isgroup.biz/

[1] http://www.ocztechnologyforum.com/forum/showthread.php?95151-Linux-patch-support-for-RevoDrive3-RevoDrive3-X2-zDrive-R4&p=686288&viewfull=1

[2] http://cateee.net/lkddb/web-lkddb/SCSI_MVSAS.html

[3] http://download.openvz.org/kernel/branches/rhel6-2.6.32/stable/

[4] http://www.ocztechnologyforum.com/forum/showthread.php?98087-OCZ-RevoDrive-3-X2-Linux-driver-AVAILABLE&p=715784&viewfull=1#post715784
