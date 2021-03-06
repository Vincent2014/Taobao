手淘H5页面商品信息爬虫test
===========
    破解淘宝js生成sign参数。
    
    新增淘宝pyppeteer登录, 有效绕过自动化工具检测。
    
思路
---------
  PC端打开手机淘宝的搜索页链接，在开发者工具中搜索到商品API，是一个GET请求。

  请求参数很多，其中最重要的三个参数为t、data、sign:

    t:  13位时间戳，很容易构造。

    data:  data参数在搜索链接重定向的url源码中，正则匹配获取。

    重点为sign参数。搜索API的initiator 调用栈可以找到sign参数的js生成函数，
    断点调试后可知该生成函数需要的变量字符串为 'cookies的token' + '&' + t + appKey + '&' + data。
    appKey为一个固定值'12574478'，t、data构造也很简单，所以接下来只要调用execjs库执行sign参数的js生成函数即可。
    
解释说明
--------
  搜索链接为手淘搜索分享的链接，未实现搜索链接的关键词构造。

  cookies中的token有时效性，过期时页面响应为“令牌过期”，此时需要更新cookies。

  脚本中代理未启用，如需大量爬取，请使用稳定高效的代理。
    
结果展示
--------
![image](https://github.com/xzh0723/Taobao/blob/master/view/pycharm_1.png)
![image](https://github.com/xzh0723/Taobao/blob/master/view/pycharm_2.png)
![image](https://github.com/xzh0723/Taobao/blob/master/view/pycharm_3.png)
![image](https://github.com/xzh0723/Taobao/blob/master/view/db.png)

公告
========
该脚本仅供学习交流，切勿用作商业用途，否则后果自负。
