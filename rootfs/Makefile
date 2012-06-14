# sudo apt-get install mtd-utils

#boot arguments for ubifs image ("ubi.mtd=2" also works)
ubibootarg = "setenv bootargs console=ttySAC0,115200 ubi.mtd=rootfs root=ubi0:rootfs rootfstype=ubifs init=/linuxrc debug"

#boot arguments for yaffs2 image
yaffsbootarg = "setenv bootargs console=ttySAC0,115200 root=/dev/mtdblock2 rootfstype=yaffs2  init=/linuxrc debug"

PATH += :../tools

all : qtopia-rootfs.yaffs2 qtopia-rootfs.ubifs

qtopia-rootfs.yaffs2 : qtopia-rootfs
	mkyaffs2image $^ $@
	@echo "please update U-Boot bootargs:"
	@echo $(yaffsbootarg)

qtopia-rootfs.ubifs : qtopia-rootfs
	mkfs.ubifs -m 4096 -e 516096 -c 1024 -x none -r $^ ubifs.img
	ubinize -o $@ -m 4096 -p 512KiB ubinize.cfg
	rm -f ubifs.img
	@echo "please update U-Boot bootargs:"
	@echo $(ubibootarg)

clean:
	rm -f *.yaffs2 *.ubifs *.img

