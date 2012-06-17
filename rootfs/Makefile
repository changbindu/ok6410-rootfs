# sudo apt-get install mtd-utils
# sudo apt-get install cramfsprogs

#boot arguments for ubifs image ("ubi.mtd=2" also works)
ubibootarg = "setenv bootargs console=ttySAC0,115200 ubi.mtd=rootfs root=ubi0:rootfs rootfstype=ubifs rw init=/linuxrc debug"

#boot arguments for yaffs2 image
yaffsbootarg = "setenv bootargs console=ttySAC0,115200 root=/dev/mtdblock2 rootfstype=yaffs2 rw init=/linuxrc debug"

#boot arguments for cramfs image
cramfsbootarg = "setenv bootargs console=ttySAC0,115200 root=/dev/mtdblock2 rootfstype=cramfs init=/linuxrc debug"

#boot arguments for jffs2 image
jffs2bootarg = "setenv bootargs console=ttySAC0,115200 root=/dev/mtdblock2 rootfstype=jffs2 rw init=/linuxrc debug"

PATH += :../tools:../tools/mtd-utils-1.5.0

all : qtopia-rootfs.yaffs2 qtopia-rootfs.ubifs qtopia-rootfs.cramfs qtopia-rootfs.jffs2

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

qtopia-rootfs.cramfs : qtopia-rootfs
	mkfs.cramfs -n rootfs $^ $@
	@echo "please update U-Boot bootargs:"
	@echo $(cramfsbootarg)

qtopia-rootfs.jffs2 : qtopia-rootfs
	mkfs.jffs2 -r $^ -o $@ -e 516096 -n
	@echo "please update U-Boot bootargs:"
	@echo $(jffs2bootarg)

clean:
	rm -f *.yaffs2 *.ubifs *.img *.cramfs *.jffs2

