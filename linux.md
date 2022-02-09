# Linux commands

## OS Version
    uname -srm
    cat /proc/version
    hostnamectl

## Make archive
    tar cvf - /etc /home | gzip > test.tar.gz

## Extract archive
    gunzip < test.tar.gz | tar xvf -

## Convert file's encoding
    iconv -f UTF-8 -t CP1252 <in_file> > <out_file>

## Linux Performance Monitoring
    vmstat
    iostat

## Information about the Linux networking
    netstat -a -n

## Monitor processes
    top

## List processes
    ps -ef