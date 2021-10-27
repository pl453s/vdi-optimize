# VDI Optimize

Automatically mount VDI, zeroing every EXT partitions and compact the VDI file.  
I recommand to put this into "~/.local/bin" to call it from anywhere.

Dependencies (and packages in Ubuntu):
- qemu-nbd (provided by "qemu-utils")
- zerofree (provided by "zerofree")
- vbox-manage (provided by "virtualbox")

To fully exploit this tool:
- Avoid logical partitions
- Do not encrypt your partitions
- Avoid having multiple large partitions
- Prefer multiples VDI files for large partitions
- Format your large partition in EXT4
- Place your large partition at the end
- Fill all available space with your large partition

Right examples:
- ```[ EFI ][ ------ ROOT ------ ]```.vdi
- ```[ EFI ][ ------ ROOT ------ ]```.vdi + ```[ --- HOME --- ]```.vdi
- ```[ EFI ][ BOOT ][ ------ ROOT ------ ]```.vdi
- ```[ BOOT ]```.vdi + ```[ --- HOME --- ]```.vdi + ```[ --- VAR --- ]```.vdi
- ```------ EXT4 (without partition table) ------```.vdi

Wrong examples:
- ```[ EFI ][ ------ ROOT ------ ][ --- FREE SPACE --- ]```.vdi
- ```[ EFI ][ BOOT ][ ------ LUKS ROOT ------ ]```.vdi
- ```[ EFI ][ BOOT ][ ------ LVM ROOT ------- ]```.vdi
- ```[ EFI ][ ------ ROOT ------ ][ --- HOME --- ]```.vdi
- ```[ EFI ][ ------ ROOT ------ ][ BOOT ]```.vdi
- ```[ EFI ][ ------  WINDOWS 10 (NTFS) ------ ]```.vdi
