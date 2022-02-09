# OS Version
    uname -srm
    cat /proc/version
    hostnamectl

## Make archive
    tar cvf - /etc /home | gzip > test.tar.gz

## Extract archive
    gunzip < test.tar.gz | tar xvf -