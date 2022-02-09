# Sun Solaris commands

## OS Version
    uname -a
    oslevel
    isainfo -v
    more /etc/release

## Restart sendmail
    # /etc/init.d/sendmail stop
    # /etc/init.d/sendmail start

## NFS client
    showmount -e hostname
    mount points /etc/vfstab
    mountall -F nfs

## NFS Server
    shareall
    share points /etc/dfs/dfstab

## File open limits
    ulimit -n 4096

## Replace carriage return "Ctrl V M" and others
    tr -d '\r\032' < $t.ux > $t

## Cpu info
    usr/platform/sun4u/sbin/prtdiag -v
    /usr/sbin/psrinfo -v

## Eeject cdrom if device busy
    # fuser -ck /cdrom 
    # fuser -ck /cdrom/cdrom0

## Information about service instances
    # svcs -a|grep nfs

## Show disks / info
    /opt/SUNWsscs/sbin/sccli
    sccli> show disk
    sccli> show media-check
    sccli> show redundancy

## Disk utilization information
    iostat -E

## Display the number of used and free i-nodes
    df -F ufs -o i

## Display processes with the highest CPU utilization
    ps -eo pid,pcpu,args | sort +1n

## Display processes with the highest memory usage
    ps -eo pid,vsz,args | sort +1n

## Printing disk geometry and partition info
    prtvtoc /dev/rdsk/c0t0d0s0

## Checking whether it's running in 32-bit mode or 64-bit mode
    isalist -v

## Verifying a route to a specified network
    # route -n get xxx.yyy.zzz.0

## Print the version of OBP
    prtconf -V

## Print the version of Open Windows
    showrev -w

## To determine which monitor resolution is available
    /usr/sbin/ffbconfig -res \?

## Display system configuration
    /usr/platform/`uname -i`/sbin/prtdiag
    sysdef

## Display the device list (and drivers attached to devices)
    prtconf -D

## Processor type, speed
    psrinfo -v

## Patch applied on the system
    showrev -p

## Exported file system on NFS server
    showmount -e NFS_SERVER

## Display current run level
    who -r

## Find out a package which a file belongs to
    pkgchk -l -p /usr/lib/sendmail

## Examining gcc behavior
    gcc -v -x c /dev/null

## Display the version of CDE
    /usr/ccs/bin/what /usr/dt/bin/dtmail

## Display the version of BIND
    nslookup -class=chaos -q=txt version.bind ns0.optix.org

## Shutdown server
    # umount /<mountings>
    # /opt/SUNWsscs/sscsconsole/sbin/sccli
    sccli> selected device /dev/rdsk/<device>
    sccli> shutdown controller
    sccli> exit
    # init 0