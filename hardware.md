# Hardware Stuff
## Rescan PCI Bus - I.E. Hot adding new hardware etc.
` # echo 0 > /sys/bus/pci/rescan `

## Rescan whole SCSI Bus - I.E. adding a new Block device or path and it hasn't been picked up and you don't know where it is (last resort - potentially disruptive) - replace 'hostH' with the HBA in question

- ` # lsscsi `
- ` # cat /proc/scsi/scsi# `  Note; scsi# is the host to use.
- ` # echo "- - -" > /sys/class/scsi_host/hostH/scan  `

## Adding a LUN Path non disruptively (DEFINITELY NOT COMPLETE)
where hosth - HBA, c - channel, t - target ID, l - lun
` echo "c t l" > /sys/class/scsi_host/hosth/scan `

## Rescan Block Device - I.E a block device has been expanded and you want to read the new capacity
` # echo 1 > /sys/block/$DEVICE/device/rescan `

## Remove block device - I.E when removing a LUN, or removing a disk from a server
` # echo 1 > /sys/block/$DEVICE/device/delete `

## Remove PCI device - I.E. nicely removing a hot swappable part.

- ` # lspci | grep -i "whatever device type you want to remove" `
- ` # find /sys -name *00:02.0 `
- ` # echo 1 > /sys/devices/$PCI-BUS/0000:$DEVICE_ID/remove `

