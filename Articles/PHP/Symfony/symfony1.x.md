symfony1.x  
----------

### SQL - Criteria
<table>
    <thead>
        <td>SQL</td>
        <td>Criteria</td>
    </thead>
    <tbody>
        <tr>
            <td>WHERE column = value</td>
            <td>->add(column, value);</td>
        </tr>
        <tr>
            <td>WHERE column <> value</td>
            <td>->add(column, value, Criteria::NOT_EQUAL);</td>
        </tr>
        <tr>
            <td>></td>
            <td>Criteria::GREATER_THAN</td>
        </tr>
        <tr>
            <td><</td>
            <td>Criteria::LESS_THAN</td>
        </tr>
        <tr>
            <td>>=</td>
            <td>Criteria::GREATER_EQUAL</td>
        </tr>
        <tr>
            <td><=</td>
            <td>Criteria::LESS_EQUAL</td>
        </tr>
        <tr>
            <td>IS NULL</td>
            <td>Criteria::ISNULL</td>
        </tr>
        <tr>
            <td>IS NOT NULL</td>
            <td>Criteria::ISNOTNULL</td>
        </tr>
        <tr>
            <td>LIKE</td>
            <td>Criteria::LIKE</td>
        </tr>
        <tr>
            <td>ILIKE</td>
            <td>Criteria::ILIKE</td>
        </tr>
        <tr>
            <td>IN</td>
            <td>Criteria::IN</td>
        </tr>
        <tr>
            <td>NOT IN</td>
            <td>Criteria::NOT_IN</td>
        </tr>
        <tr><td colspan="2">Other SQL Keywords</td></tr>
        <tr>
            <td>ORDER BY column ASC</td>
            <td>->addAscendingOrderByColumn(column);</td>
        </tr>
        <tr>
            <td>ORDER BY column DESC</td>
            <td>->addDescendingOrderByColumn(column);</td>
        </tr>
        <tr>
            <td>GROUP BY column DESC</td>
            <td>->addGroupBy(column);</td>
        </tr>
        <tr>
            <td>LIMIT limit</td>
            <td>->setLimit(limit)</td>
        </tr>
        <tr>
            <td>OFFSET offset</td>
            <td>->setOffset(offset)</td>
        </tr>
        <tr>
            <td>FROM table1, table2 WHERE table1.col1 = table2.col2</td>
            <td>->addJoin(col1, col2);</td>
        </tr>
        <tr>
            <td>FROM table1 LEFT JOIN table2 ON table1.col1 = table2.col2</td>
            <td>->addJoin(col1, col2, Criteria::LEFT_JOIN)</td>
        </tr>
        <tr>
            <td>FROM table1 RIGHT JOIN table2 ON table1.col1 = table2.col2</td>
            <td>->addJoin(col1, col2, Criteria::RIGHT_JOIN)</td>
        </tr>
    </tbody>
</table>

### 使用InnoDB(Use InnoDB with Propel)
[原文地址](http://snippets.symfony-project.org/snippet/1)  
To enable InnoDB support in Propel, you can add this line at the end of your config/propel.ini configuration file:
<pre>
propel.mysql.tableType = InnoDB
</pre>

### 使用事务(Use transaction in the model)
[原文地址](http://snippets.symfony-project.org/snippet/2)  
<pre>
$con = Propel::getConnection();
try{
  $con->begin();
 
  // do something
 
  $con->commit();
}catch (Exception $e){
  $con->rollback();
  throw $e;
}
</pre>

### 在脚本中使用model(Use the model in a batch or a test)
[原文地址](http://snippets.symfony-project.org/snippet/6)  
To use database connections defined in the databases.yml configuration file, you can use the following snippet:
<pre>
// initialize database manager
$databaseManager = new sfDatabaseManager();
$databaseManager->initialize();
</pre>

### 在action中隐藏debug bar(Hide debug screen by actions)
[原文地址](http://snippets.symfony-project.org/snippet/10)  
<pre>
sfConfig::set('sf_web_debug', false);
</pre>

### 获取数据库连接(Fetch database connection)
[原文地址](http://snippets.symfony-project.org/snippet/11)  
<pre>
$connection = sfContext::getInstance()->getDatabaseConnection('propel');

//or

$connection = Propel::getConnection();
</pre>

### turn on form repopulation
[原文地址](http://snippets.symfony-project.org/snippet/15)  
add this to your validation file for the action.
eg: indexSuccess.php would have have a file called index.yml in the validate directory for that module if you configured validation.
<pre>
fillin:
  activate: on   # activate the form repopulation
  param:
    name: test   # name of the form
</pre>

### doUpdate
[原文地址](http://stackoverflow.com/questions/12282832/update-multiple-rows-with-propel-1-4)  

<pre>
$criteria=new Criteria()
$criteria->add(NotificationPeer::TO, $memberId, Criteria::EQUAL);
$criteria->add(NotificationPeer::ACTION, 0, Criteria::EQUAL);
$notification = NotificationPeer::doSelect($criteria);

foreach($notification as $notice){
    $notice->setRead(1);
    $notice->save();
}

// we should use

$selectCriteria = new Criteria();
$selectCriteria->add(NotificationPeer::TO, $memberId, Criteria::EQUAL);
$selectCriteria->add(NotificationPeer::ACTION, 0, Criteria::EQUAL);

$updateCriteria = new Criteria();
$updateCriteria->add(NotificationPeer::READ, 1);

BasePeer::doUpdate($selectCriteria, $updateCriteria, $con);
</pre>
