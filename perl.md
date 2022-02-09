# Perl commands

## Find the "age" of a file
    perl -e '$mtime = (stat($ARGV[0]))[9];
    $age = ($mtime) ? time - $mtime : -1;
    print "$age\n";' file_name