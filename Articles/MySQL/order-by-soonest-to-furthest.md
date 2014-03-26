Order by soonest to furthest  
----------------------------

我们在如果在做运动比赛(ie:soccer)赛程的时候, 大部分时间前台的排序我们希望是:  
- 还未进行的比赛, 需要从离现在最近排到离现在最远   
- 已经进行的比赛, 也需要离现在最近排到离现在最远  
*Sample*  

game表有如下数据  
id, event_date  
1, 2013-03-28  
2, 2014-04-03  
3, 2014-03-29  
4, 2014-02-22  
5, 2014-02-25  

我们想要得到的结果是  
1, 2013-03-28  
3, 2014-03-29  
2, 2014-04-03  
5, 2014-02-25  
4, 2014-02-22  

这时候SQL应该是

<pre>
SELECT id, event_date
  FROM game
  ORDER BY IF(event_date &lt; NOW(), 0, 1) DESC,
  ABS(DATEDIFF(event_date, NOW())) ASC;
</pre>
