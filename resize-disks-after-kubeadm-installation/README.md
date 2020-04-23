After successful installation you can resize you disk as it is by default 10GB per each node.

Here is the easiest and reliable way to do it:

Go to each directory that has the vmdk storage per each node and do the commands below.

1) Clone the disks to VDI format
VBoxManage clonemedium disk ubuntu-bionic-18.04-cloudimg.vmdk k8s-master.vdi --format VDI
VBoxManage clonemedium disk ubuntu-bionic-18.04-cloudimg.vmdk node-1.vdi --format VDI
VBoxManage clonemedium disk ubuntu-bionic-18.04-cloudimg.vmdk node-2.vdi --format VDI

2) resize the disks as master 40GB, and each node by 20GB:
VBoxManage modifymedium disk k8s-master.vdi --resize 40960
VBoxManage modifymedium disk node-1.vdi --resize 20480
VBoxManage modifymedium disk node-2.vdi --resize 20480

3) reformat the VDI to VMDK format 
VBoxManage clonemedium disk k8s-master.vdi k8s-master.vmdk --format VMDK
VBoxManage clonemedium disk node-1.vdi node-1.vmdk --format VMDK
VBoxManage clonemedium disk node-2.vdi node-2.vmdk --format VMDK
rm -f k8s-master.vdi node-1.vdi node-2.vdi node

4) Download gpard iso and resize the partions to get the full resized disk
Download gpard iso for amd64: https://gparted.org/download.php
Maximize the partition sizes .


  createmedium              [disk|dvd|floppy] --filename <filename>
                            [--size <megabytes>|--sizebyte <bytes>]
                            [--diffparent <uuid>|<filename>
                            [--format VDI|VMDK|VHD] (default: VDI)
                            [--variant Standard,Fixed,Split2G,Stream,ESX]

  modifymedium              [disk|dvd|floppy] <uuid|filename>
                            [--type normal|writethrough|immutable|shareable|
                                    readonly|multiattach]
                            [--autoreset on|off]
                            [--property <name=[value]>]
                            [--compact]
                            [--resize <megabytes>|--resizebyte <bytes>]
                            [--move <path]
                            [--description <description string>]
							
  clonemedium               [disk|dvd|floppy] <uuid|inputfile> <uuid|outputfile>
                            [--format VDI|VMDK|VHD|RAW|<other>]
                            [--variant Standard,Fixed,Split2G,Stream,ESX]
                            [--existing]

