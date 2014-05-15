Query Dump to CSV  
-----------------

在有的时候我们需要导出一张表的一些数据, 而不是所有数据  

###方法1  
<pre>
mysqldump -hxxx -uxxx -pxxx database_name table_name --where="column=141" > querydump.sql
</pre>

###方法2  
<pre>
SELECT * FROM table_name WHERE column = 141
INTO OUTFILE '/home/jmao/querydump.csv'
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
</pre>