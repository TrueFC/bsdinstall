# bsdinstall

This is a patch for those installing with installerconfig on FreeBSD. The current 
because at the time there is less of a problem in bsdinstall, ZFS does not
install properly when zpool separate to bootpool and zroot. This patch
overcome this problem. This has already been 
reported to [Bug 229628] (https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=229628#attach_194980) . 

## Contents of the bug

#### 1. Since /boot is symbolically linked to /bootpool, it is  
expanded by

	 # tar - xf distrubution_tarball - C chroot_directory 

in script so it will not be expanded to /bootpool. This 
can be solved by adding the -P option to tar. 

#### 2. bootpool's zpool.cache information does not contain bootpool information
and zroot's zpool.cache does not exist, bootpool will not be imported at
boot time and will not boot properly. To solve this problem create
zpool.cache with bootpool and zroot in /boot/zfs/zpool.cache with
zpsboot on bootpool after creating bootpool, and on zroot as well
zpool.cache in /boot/zfs/zpool.cache. 

## Tag update history 

* **13.0-CURRENT-r339677** (Wed 12 Dec 2018 07:25:34)

	FreeBSD 13.0-CURRENT for revision 339677
