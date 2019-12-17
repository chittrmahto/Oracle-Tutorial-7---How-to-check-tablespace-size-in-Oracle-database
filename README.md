# Oracle-Tutorial-7---How-to-check-tablespace-size-in-Oracle-database
Oracle Tutorial 7 - How to check tablespace size in Oracle database


Steps: ---
1. Login to your Oracle Database. (sqlplus / as sysdba)
2. run the below commands.
 
  For setting the tablespae colum format.
  SQL> col TABLESPACE_NAME format a20

  for set the lines.
  SQL> set lines 900

  Now copy the below code and paste in oracle cmd.
  SQL> select avail_tname "TABLESPACE_NAME",sum(round(avail_space,2)) "ALLOCATED (MB)",((round(avail_space,2)-round(free_space,2))) "USED (MB)",(round(free_space,2)) "FREE (MB)",(round(((round(avail_space,2)-round(free_space,2))/avail_space)*100,2)) "USED (%)",(round((free_space/avail_space)*100,2)) "FREE (%)" from (select tablespace_name avail_tname,sum(bytes)/1024/1024 avail_space from dba_data_files group by tablespace_name) a,(select tablespace_name free_tname,sum(bytes)/1024/1024 free_space from dba_free_space group by tablespace_name) b where a.avail_tname=b.free_tname group by avail_tname,avail_space,free_space UNION all select avail_tname "TABLESPACE  NAME",sum(round(avail_space,2)) "ALLOCATED (MB)",((round(avail_space,2)-round(free_space,2))) "USED (MB)",(round(free_space,2)) "FREE (MB)",(round(((round(avail_space,2)-round(free_space,2))/avail_space)*100,2)) "USED (%)",(round((free_space/avail_space)*100,2)) "FREE (%)" from (select tablespace_name avail_tname,sum(bytes)/1024/1024 avail_space from dba_temp_files group by tablespace_name) a,(select tablespace_name free_tname,sum(bytes_free)/1024/1024 free_space from v$temp_space_header group by tablespace_name) b where a.avail_tname=b.free_tname group by avail_tname,avail_space,free_space order by 5 desc;



The above command give you the list of tablespace with size details like allcated, used, free and Percentages also.



Video URL : https://chittranjanmahto.blogspot.com/2019/08/oracle-tutorial-7-how-to-check.html
