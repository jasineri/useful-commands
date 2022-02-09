## Make archive
    tar cvf - /etc /home | gzip > test.tar.gz
## Extract archive
    gunzip < test.tar.gz | tar xvf -

## Replace carriage return "ctrl V M" and others
    tr -d '\r\032' < $t.ux > $t