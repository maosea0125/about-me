Query Dump to CSV  
-----------------

���е�ʱ��������Ҫ����һ�ű��һЩ����, ��������������  

###����1  
<pre>
mysqldump -hxxx -uxxx -pxxx database_name table_name --where="column=141" > querydump.sql
</pre>

###����2  
<pre>
SELECT * FROM table_name WHERE column = 141
INTO OUTFILE '/home/jmao/querydump.csv'
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
</pre>