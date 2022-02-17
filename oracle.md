# Oracle commands

## Kill sessions
    SELECT 'ALTER SYSTEM KILL SESSION '''||sid||','||serial#||''' IMMEDIATE;' FROM v$session;