# DB2 commands

## DB2 version
    db2level
    db2licm -l
    pkginfo -l db2cliv71

## Generate support request
    db2support . -g -s

## Verify the table pd for corruption:
    db2cat -d <db> -n <table> -s <schema> -o db2cat0.out

## Check Dependencies
    select constname from SYSCAT.REFERENCES where TABNAME like 'TABNAME%' or REFTABNAME like 'TABNAME%';
    select viewschema,viewname from SYSCAT.VIEWDEP where BSCHEMA like 'SCHEMANAME%' and BNAME like 'TABNAME%';
    select funcschema,funcname from SYSCAT.FUNCDEP where BSCHEMA like 'SCHEMANAME%' and BNAME like 'TABNAME%';
    select constname from SYSCAT.CHECKS where TABSCHEMA like 'SCHEMANAME%' and TABNAME like 'TABNAME%';
    select constname from SYSCAT.REFERENCES where TABSCHEMA like 'SCHEMANAME%' and TABNAME like 'TABNAME%';
    select trigschema,trigname from SYSCAT.TRIGDEP where BSCHEMA like 'SCHEMANAME%' and BNAME like 'TABNAME%'; 

## Lists entries in the history file:
    db2 list history DROPPED TABLE ALL for <Database>

## Lock table in exclusive mode
    LOCK TABLE "<Table>" IN EXCLUSIVE MODE

## Get DB2 task run history
    select * from "TOOLSCAT"."MDTHISTORYTY00"
    where START00 > '2009-02-04 00:00:00.0000'
    and taskname00='<Taskname>'

## DB2 Administration Server Command
    # su - <dasusr>
    $ db2admin stop
    $ db2admin start

## Configure Replication Monitor
    asnpwd encrypt all
    asnpwd add alias <Database> id db2admin password xyxyxyxyxxyyx
    asnpwd add alias <Database> id db2admin password xyxyxyxyxxyyx

## Database size
    db2 "CALL GET_DBSIZE_INFO(?, ?, ?, 0)"

## Restore tablespace
    db2 update db cfg using LOGRETAIN ON
    db2stop force
    db2start
    db2 "restore db <Database> TABLESPACE (TS_REFERENCE) from /<path_to_backup> TAKEN AT 20071029094805"

## Check backup / restore status
    db2 list utilities show detail

## Restore progress
    db2 list utilities show detail
    db2 rollforward database <Database> query status

## Show information
    db2pd -db <Database>
    db2pd -db <Database> -tablespaces

## Archive db2log
    db2diag -A

## DB2 backup / restore
    db2 backup db <Database> online to /<path_to_backup> include logs
    db2 restore db <Database> from /<path_to_backup> TAKEN AT 20070126174124 INTO <Database> logtarget /<path_to_backup> REPLACE EXISTING
    db2 "rollforward db <Database> to end of logs and stop OVERFLOW LOG PATH (/<path_to_backup>)"
    db2 RESTORE DATABASE <Database> FROM /<path_to_backup> TAKEN AT 20070126171443 INTO <Database> REPLACE EXISTING WITHOUT ROLLING FORWARD
    db2 restore db <Database> from /<path_to_backup> taken at 20060724140400 into <Database> REPLACE EXISTING WITHOUT ROLLING FORWARD WITHOUT PROMPTING
    db2 restore db <Database> from /<path_to_backup> taken at 20060706143513 into <Database> WITHOUT PROMPTING
    db2 rollforward db <Database> to end of logs and complete

## Remove carriage returns
    replace(COP_MESSAGE,x'26','')

## Date transformation
    DATE(TRANSLATE('EF/GH/ABCD',substr(PRMYYYYMM,2)||'01','ABCDEFGH'))


## Replication. Force a full refresh by resetting the LASTSUCCESS, SYNCHTIME, and SYNCHPOINT values in subscription set table to null.
    -- on source database
    update ASN.IBMSNAP_PRUNCNTL
    set SYNCHTIME = null, SYNCHPOINT = null
    WHERE SOURCE_TABLE='<Tablename>'

    -- on target database
    UPDATE ASN.IBMSNAP_SUBS_SET
    SET LastSuccess = NULL,
    SynchPoint = NULL,
    SynchTime = NULL
    WHERE set_name = 'STY';

## Find table's columns
     SELECT C.TABSCHEMA, C.TABNAME,
            C.COLNAME
        FROM SYSCAT.TABLES AS T,
             SYSCAT.COLUMNS AS C
        WHERE T.TBSPACEID = n1
        AND T.TABLEID = n2
        AND C.COLNO = n3
        AND C.TABSCHEMA = T.TABSCHEMA
        AND C.TABNAME = T.TABNAME

## Update allocation parameters + monitor
    db2 update dbm cfg using DFT_MON_SORT off DFT_MON_STMT off DFT_MON_BUFPOOL off
    db2 update db cfg for <Database> using sortheap 1024

## Get DB config
    db2 get db cfg for <Database>

## Update log file size
    db2 update db cfg for <Database> USING LOGFILSIZ 40000
    db2 update db cfg for <Database> USING LOGSECOND 100

## Check status
    SYSCAT.TABLES (Columns STATUS: C -> 'Check Pending')

## Replication trace
    tail /home/db2admin/utilogs/STUDY.TRC|grep -i UP1SYT

## Checks the status of a load operation
    db2 load query

## Restart database, force kill all connections!
    DEACTIVATE DATABASE database-alias

## List user defined Jars
    ls /home/db2admin/sqllib/function/jar/DB2ADMIN

## Large archive
    cat <archive_name>.001 | unix2dos | gzip -c > backup.gz

## Capture erorrs
    db2 "select * from ASN.IBMSNAP_TRACE where TRACE_TIME >'2004-04-13-11.00.00.000000' order by TRACE_TIME"

## Start JDBC daemons
    db2start
    db2jstrt
    db2jd <Portnumber>

## Extend tablespace
    db2 "alter TABLESPACE <Name> EXTEND (FILE '/<path_to_file>.dbm' 6G)"

## Find db2 processes
    ps -ef|grep db2|grep -v db2sysc|grep -v db2jd|grep -v bash

## Get backup pending databases
    db2 "get db cfg for <Database>" | grep -i "BACKUP PENDING"

## List tablespaces
    db2 list tablespaces show detail

## Monitor instances
    while (db2list) do sleep 10; date; done

## Get snapshot for application
    db2 "GET SNAPSHOT FOR APPLICATION AGENTID <Nr>"|grep "Rows updated"

## Get Db2 diagnostic log 
    tail /home/db2admin/sqllib/db2dump/db2diag.log

## List applications
    db2 "list applications show detail"

## Get snapshot for application
    db2 "GET SNAPSHOT FOR APPLICATION AGENTID (Appl. Handle)"

## Explain plan for ...(select statement)
    db2exfmt -> <Database>

## Force application
    db2 "force application (Appl. Handle)"

## Generate DDL
    db2look -d <Database> -e -l -x -f -a -o db2look.sql
    db2look -d <Database> -t <Tablespace> -o dap.txt -e
    db2look -d <Database> -o dap.txt -e

## List tables
    db2 "select tbspace,index_tbspace from sysibm.systables where lower(NAME) like '...'"

## List indexes
    db2 "select * from sysibm.sysindexes where lower(TBNAME) like '...'"

## Invalid / inoperative views:
    db2 "select name from sysibm.sysviews where valid='X'"
    select text||';' from sysibm.sysviews where valid='X';

## Drop database
    db2 connect reset
    db2 drop database <Database>

## parameter commit
    db2 parameter commit-

## Export / import data
    export to <Filename>.ixf of ixf select * from <Tablename>;
    load from <Filename>.ixf of ixf replace into <Tablename> nonrecoverable;

## Scheduled tasks appear as running in the Scheduler even though they have completed
When DAS is brought down while a scheduled task is running, the status of the task might stay in 'running' state even though the job has already finished or was aborted.

Solution to remove the hanged 'running' tasks from the Scheduler:

1. Locate the 'running' record(s) by getting the corresponding task ID, which can be obtained from the Task Center.

2. Stop the DAS.

3. Run these commands:

        db2 connect to TOOLSDB
        db2 delete from SYSTOOLS.MDTASKEXECTY00 where taskID=<Nr>

4. Restart DAS and the Scheduler to check if the 'running' jobs are removed. If not, proceed to step 5.

5. Make sure DAS is stopped again.

6. Issue these commands:

        db2 connect to TOOLSDB
        db2 update SYSTOOLS.MDTASKTYPE00 set NUMBEROFEXECUTIONS00=0
        db2 update SYSTOOLS.MDTASKTYPE00 set STATE00='0'

7. Restart DAS and the Scheduler. The 'running' tasks should be removed.