# planning before install
use as the sever we should consider:
- the electrical costing, since the server is running 24 hours a day
- if the hardware's producor provide the dirver for linux

hardware:
- **cpu:** intel i3 series
- **ram:** more than 512m
- **hard disk:** more than 20g
- **vga:** the graphic memory need above 32m

disk partition：
- **name of sata:** the name of sata is depended on the which sata be read by cpu
- **partition table:** 
    * MSDOS(MBR): at the frist sector 512bytes contained **MBR(446bytes)**and**partition table(64bytes)** which have **four recording areas**, its recorded the begin number and the end number of the cylinder
    * recording areas: include Primary and Extended partition, Extended partition is used to logical parted. The one dish can only have one Extend partition, its usually in the end space of disk. logical partition can not be formation
    > Each group of partiton table only have 16bytes so it can only record below 2.2Tb capacity of the disk

    * **GPT:** because now the capacity of sector is grows to 4Kb, to compatible the 512byte's sector **GPT** use the LBA(Logical Block Address) to record, the LBA is initialized 512bytes
    * **LBA0:** compatible with MBR. **LBA1:** record each partition table's address and size. **LBA2-33:** record partition information. Each LBA's size is 512bytes, it can record 4 partition. it use 64byte to record the number of sector
    > Each LBA can formation. used gdisk to parted the GPT, after grub2 can recgnized GPT 

- BIOS and UEFI(vbird_book p142)
