propel-build-sql  
----------

**Problem**   
我们在使用symfony的propel-build-sql的时候，默认生成的SQL是TYPE=InnoDB，但是在新版本的MySQL中却是ENGINE=InnoDB，导致我们使用propel-insert-sql的时候就无法插入SQL.

这时我们只需要修改  
/lib/vendor/propel-generator/classes/propel/engine/builder/sql/mysql/MysqlDDLBuilder.php文件145行，将Type修改为ENGINE即可