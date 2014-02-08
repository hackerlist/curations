# QuickBooks for the Linux User

Or how a linux user spent more time than anyone should failing
in most possible ways to configure Windows & Quickbooks over
Linux KVM.

## Index:

- Drawbacks of Quickbooks Online
- Setup VM (KVM), Ubuntu

## Quickbooks Online

I started with Quickbooks online. At the time (Dec 2013) there
was no way to import/pull bank data prior to ~3 months. Also,
it required Active X and IE 10+ to export data.

## Setup a Windows VM

Setup KVM and (optionally) virt gui:
[https://wiki.debian.org/KVM]

    $ aptitude install qemu-kvm libvirt-bin
    $ sudo apt-get install virt-manager virt-viewer # (optional)


### Download an .iso:

Attempt 1: I choose windows xp as the image because it was
smaller and I had the image already. Download Windows 7 or
higher .iso. Avoid XP as support is deprecated as of 2014 and
XP is unable to run IE higher than 8 which causes problems w/
some quickbooks interfaces.

### Create your vm image .img:

Refer to
[http://www.howtoforge.com/installing-windows-xp-as-a-kvm-guest-on-ubuntu-8.10-desktop]. 25
GB HDD space is recommended as Windows is 15+GB bas install
and 7 SP1 requires 5GB, which is a requirement for IE 11.

    $ dd if=/dev/zero of=~/win7.img	bs=1024k count=20000

### Startup the vm

It's recommended that you start your vm with 3500mb of RAM
(x86-32) or 4096+ (amd/x86-64) as Quickbooks requires at least
1GB free Ram.

    $ kvm -m 512 -cdrom ~/win7.iso -boot d ~/win7.img

## Installing Quickbooks

1. Win7 SP 1
2. IE 11
3. Quickbooks - if you get an iso
   (http://blogs.technet.com/b/odsupport/archive/2011/04/19/how-to-extract-the-contents-from-an-iso-file-without-burning-the-iso-to-disc.aspx)

## Out of space? Resize the vm.

http://www.linux-kvm.com/content/how-resize-your-kvm-virtual-disk

    $ qemu-img resize win7.img +5GB
