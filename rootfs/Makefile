# sudo apt-get install mtd-utils

PATH += :../tools

all : qtopia-rootfs.yaffs2 qtopia-rootfs.ubifs

qtopia-rootfs.yaffs2 : qtopia-rootfs
	mkyaffs2image $^ $@

qtopia-rootfs.ubifs : qtopia-rootfs
	mkfs.ubifs -m 2048 -e 128KiB -c 1024 -r $^ $@
