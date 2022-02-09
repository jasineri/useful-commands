# OS Version
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