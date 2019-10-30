# memsql_pipeline_offset_summary
memsql pipeline offset summary 

will update as a view once cross-db views are GA

```
memsql> select database_name, pipeline_name, source_type, format(sum(latest_offset)-sum(successful_cursor_offset),0) as offset_backlog, round(unix_timestamp()-max(UPDATED_UNIX_TIMESTAMP),2) as seconds_since_last_update from information_schema.PIPELINES_CURSORS group by 1,2,3 order by 1,2;
+---------------+-------------------+-------------+----------------+---------------------------+
| database_name | pipeline_name     | source_type | offset_backlog | seconds_since_last_update |
+---------------+-------------------+-------------+----------------+---------------------------+
| utility       | ami_reads         | KAFKA       | 4,316,996      |                    275.13 |
| utility       | transformer_scada | KAFKA       | 0              |                    740.93 |
| utility       | voltage_reads     | KAFKA       | 0              |                      2.40 |
+---------------+-------------------+-------------+----------------+---------------------------+
3 rows in set (0.00 sec)
```
