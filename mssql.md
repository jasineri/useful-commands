# MS SQL commands

## List views columns with types
    SELECT Schema_name(v.schema_id) AS schema_name,
       Object_name(c.object_id) AS view_name,
       c.column_id,
       c.name                   AS column_name,
       Type_name(user_type_id)  AS data_type,
       c.max_length,
       c.precision,
       c.is_nullable
    FROM   sys.columns c
       JOIN sys.views v
         ON v.object_id = c.object_id
    WHERE lower(Object_name(c.object_id)) like '...'
    ORDER  BY schema_name,
          view_name,
          column_id; 

## List sessions / active connections
    exec sp_who2
