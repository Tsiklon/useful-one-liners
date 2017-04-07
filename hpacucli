Hpacucli Utility for Linux - All Commands Guide
Information

This information will help the user on how one can use the hpacucli utility for linux to add, delete, identify and repair logical and physical disks on the Smart array controller.
Details

hpacucli utility:

    # hpacucli

    # hpacucli help

NOTE: User can use the hpacucli command in a script after installing hpacucli package (can be download separately as rpm / it also comes in PSP in Linux).

    Controller commands:

    hpacucli> ctrl all show config                  ## Display detail of Controller  

    hpacucli> ctrl all show config detail

    hpacucli> ctrl all show status                  ## Display status of Controller

    hpacucli> ctrl slot=0 modify dwc=disable         ## Enable or Disable the cache  

    hpacucli> ctrl slot=0 modify dwc=enable

    hpacucli> rescan           ## Detects newly added devices since the last rescan

    Physical drive commands:

    hpacucli> ctrl slot=0 pd all show ## Display detail information of PhysicalDrive  hpacucli> ctrl slot=0 pd 2:3 show detail

    hpacucli> ctrl slot=0 pd all show status      ## Display Status of physicalDrive  hpacucli> ctrl slot=0 pd 2:3 show status

    hpacucli> ctrl slot=0 pd 2:3 modify erase          ## To Erase the physicalDrive

    hpacucli> ctrl slot=0 pd 2:3 modify led=on       ## To enable or Disable the LED  hpacucli> ctrl slot=0 pd 2:3 modify led=off

    Logical drive commands:

    hpacucli> ctrl slot=0 ld all show   ## Display detail information of LogicalDrive  hpacucli> ctrl slot=0 ld 4 show

    hpacucli> ctrl slot=0 ld all show status        ## Display Status of LogicalDrive  hpacucli> ctrl slot=0 ld 4 show status

    hpacucli> ctrl slot=0 ld 4 modify reenable forced  ## To re-enabling failed drive

Configuring RAID level:

    Create LogicalDrive with RAID 0 using one drive:

    hpacucli> ctrl slot=0 create type=ld drives=1:12 raid=0   

    Create LogicalDrive with RAID 1 using two drives:

    hpacucli> ctrl slot=0 create type=ld drives=1:13,1:14 size=300 raid=1

    Create LogicalDrive with RAID 5 using five drives:

    hpacucli> ctrl slot=0 create type=ld drives=1:13,1:14,1:15,1:16,1:17 raid=5

    Expand, Extend, add spare and deleting Logical drives in existing RAID:

    hpacucli> ctrl slot=0 ld 4 delete
    ## To Delete LogicalDrives

    hpacucli> ctrl slot=0 ld 4 add drives=2:3 
    ## Expanding ld by adding one more drive

    hpacucli> ctrl slot=0 ld 4 modify size=500 forced 
    ## Extending the LogicalDrives

    hpacucli> ctrl slot=0 array all add spares=1:5,1:7
    ## Add two Spare disks


