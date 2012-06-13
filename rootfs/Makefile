# sudo apt-get install mtd-utils

#boot arguments for ubifs image
#setenv bootargs console=ttySAC0,115200 ubi.mtd=2 root=ubi0:rootfs rootfstype=ubifs init=/linuxrc debug

#boot arguments for yaffs2 image
#setenv bootargs console=ttySAC0,115200 root=/dev/mtdblock2 rootfstype=yaffs2  init=/linuxrc debug

PATH += :../tools

all : qtopia-rootfs.yaffs2 qtopia-rootfs.ubifs

qtopia-rootfs.yaffs2 : qtopia-rootfs
	mkyaffs2image $^ $@

qtopia-rootfs.ubifs : qtopia-rootfs
	mkfs.ubifs -m 4096 -e 516096 -c 1024 -x none -r $^ ubifs.img
	ubinize -o $@ -m 4096 -p 512KiB ubinize.cfg

clean:
	rm *.yaffs2 *.ubifs *.img

