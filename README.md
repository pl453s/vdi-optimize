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
- ```[[ EFI ][     ROOT     ]]```
- ```[[ EFI ][     ROOT     ]]``` + ```[[   HOME   ]]```
- ```[[ EFI ][ BOOT ][     ROOT     ]]```
- ```[[ BOOT ]]``` + ```[[   HOME   ]]``` + ```[[   VAR   ]]```
- ```[     EXT4 (without partition table)     ]```

Wrong examples:
- [[ EFI ][     ROOT     ][     FREE SPACE     ]]
- [[ EFI ][ BOOT ][     LUKS ROOT     ]]
- [[ EFI ][ BOOT ][     LVM ROOT     ]]
- [[ EFI ][     ROOT     ][   HOME   ]]
- [[ EFI ][     ROOT     ][ BOOT ]]
- [[ EFI ][     WINDOWS 10 (NTFS)     ]]
