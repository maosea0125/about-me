ON DUPLICATE KEY UPDATE  
==========

> 在开发过程中, 我们经常需要对关系表进行更新操作.

下面是个例子(代码基于Symfony1.x):  
<pre>
CREATE TABLE `game_corner_kicks` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `game_id` int(11) NOT NULL,
  `player_id` int(11) NOT NULL,
  `corner_kicks` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `fk_game_id_player_id` (`game_id`,`player_id`)
) ENGINE=InnoDB;
</pre>

当我们需要更新corner_kicks字段的数据时, 我们并不清楚数据库是否已经存在这样的数据, 我们可以采用的方式有:  
> Notes: 在一场正常的比赛中, 球员有可能不是一个人, 比如足球, 双方球员加起来有22个.  

#### Bad1:  
> 这种方式我们执行的SQL将会达到44次, 这种方法性能是最差的  

<pre>
foreach($cornerKicks as $cornerKick){
    $criteria = new Criteria();
    $criteria->add(GameCornerKicksPeer::GAME_ID, 1);
    $criteria->add(GameCornerKicksPeer::PLAYER_ID, $cornerKick['player_id']);
    $gameCornerKicks = GameCornerKicksPeer::doSelectOne($criteria);
    
    if($gameCornerKicks == null) $gameCornerKicks = new GameCornerKicks();
    $gameCornerKicks->setGameId(1);
    $gameCornerKicks->setPlayerId($cornerKick['player_id']);
    $gameCornerKicks->setCornerKicks($cornerKick['corner_kick']);
    $gameCornerKicks->save();
}
</pre>

#### Bad2:
> 这种方式我们执行的SQL将会达到23次, 同样会导致自增字段id的急剧增大  

<pre>
//delete the data and insert again
$criteria = new Criteria();
$criteria->add(GameCornerKicksPeer::GAME_ID, 1);
GameCornerKicksPeer::doDelete($criteria);

foreach($cornerKicks as $cornerKick){
    $gameCornerKicks = new GameCornerKicks();
    $gameCornerKicks->setGameId(1);
    $gameCornerKicks->setPlayerId($cornerKick['player_id']);
    $gameCornerKicks->setCornerKicks($cornerKick['corner_kick']);
    $gameCornerKicks->save();
}
</pre>

#### Good:

<pre>
$sql = '';
$p   = array();

foreach($cornerKicks as $cornerKick){
    $sql .= "INSERT INTO game_corner_kicks
        (`game_id`, `player_id`, `corner_kicks`) VALUES
        (?, ?, ?) ON DUPLICATE KEY UPDATE corner_kicks = ?;";
    $p[] = 1; 
    $p[] = $cornerKick['player_id'];
    $p[] = $cornerKick['corner_kick'];
}

if($sql){
    $connection = Propel::getConnection($con);
    $statement = $connection->prepareStatement($sql);
    $statement->executeQuery($p);
}
</pre>