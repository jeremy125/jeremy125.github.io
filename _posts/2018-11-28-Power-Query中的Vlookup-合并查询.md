---
layout: post
title: 'Power Query中的Vlookup-合并查询'
date: 2018-11-28
categories: 数据分析
cover: 'https://mmbiz.qpic.cn/mmbiz_png/Ibz2ROUou9yvWGQGibgfnkEIGmAyQ19jRGzlxrX3bnGrICv5DrRxicQfr50LPq2c4XeHMIChgIZjDdnha780Do9A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'
tags: powerquery 转载 数据分析 数据清洗
---

## Power Query中的VLOOKUP - 合并查询

原创： 叶婷 [PowerPivot工坊](javascript:void(0);) *2017-11-21*

VLOOKUP是EXCEL函数里的大众情人，但是大家对TA是既爱又恨：简单方便，但是一旦数据量上升到数十万量级就开始耍小脾气了，时不时就会出现未响应，接下来我们来扒一扒Vlookup的替代方案。




在PowerPivot中我们可以创建两个表之间的关系，通过DAX中Related解决，但是虽然能够得到数据，却不能导出到EXCEL中，眼看得到了解决，却还是拿不到结果，那么我们该怎么得到结果呢？


这时，我们可以思考一个问题，我们想要的是另一表中匹配列，Vlookup就是通过查找与此相对应的数据得到匹配列，那么我们可以联想下查询中的哪些功能可以使用。突然想到Excel Power Query教程中有一节是关于生成笛卡尔积表，利用的是合并查询的功能。那么合并查询是否也能够解决现在的问题呢？


我们来试一试就知道了😍，图1是两个表，一个是人员信息表，一个是匹配表。
 



![img](https://mmbiz.qpic.cn/mmbiz_png/Ibz2ROUou9yvWGQGibgfnkEIGmAyQ19jRUsPLjfrsur4Rw6tNMojsV5p15moeCvAp5LYXdXn7QVQWZ7JyYibnQxQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



我们将这两个表导入到查询中：

![img](https://mmbiz.qpic.cn/mmbiz_png/Ibz2ROUou9yvWGQGibgfnkEIGmAyQ19jRRnnxBz0vVIqrItXKJS2ZoIjy1Iwkyd7rSXuFia5uLu40kwIKKxezo6g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

想要在人员信息表中增加入职日期信息，那么要先选中人员信息表，然后再选择匹配表，将两个表中的ID列分别选中，如下图
 

![img](https://mmbiz.qpic.cn/mmbiz_png/Ibz2ROUou9yvWGQGibgfnkEIGmAyQ19jRGzlxrX3bnGrICv5DrRxicQfr50LPq2c4XeHMIChgIZjDdnha780Do9A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



点击确定，得到以下结果

![img](https://mmbiz.qpic.cn/mmbiz_png/Ibz2ROUou9yvWGQGibgfnkEIGmAyQ19jRIljq8KLB0B1pb6GwNkrunakIicaZYiawFFe500Wsdxp7ov2jYFiajdOqA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



可以看到增加了一个新列，展开选择扩展入职日期：
 

![img](https://mmbiz.qpic.cn/mmbiz_png/Ibz2ROUou9yvWGQGibgfnkEIGmAyQ19jRtmZfFYQckPI4KdlVYyNljpwC88OsZicCWXTj1ukodic9PbtxN93VPC5w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

确定之后选择关闭并上载，就可以得到结果了，是不是又快又简单，而且如果有数据更改一键刷新就可以了，再也不用担心数据出错了，再也不用担心Vlookup的小脾气咯！！！
 

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

问题得到解决了，可是上面的步骤中应该还有一个小疑问，我们在图2中可以看到有联接种类的选项，展开可以看到如下
 

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)



总共有6个选项，那么TA们有什么区别呢？
我们用一个简单的例子来说明一下：
 

![img](https://mmbiz.qpic.cn/mmbiz_png/Ibz2ROUou9yvWGQGibgfnkEIGmAyQ19jR2MScPMOzYaySxOUHFlZfzL2Gf7qMY601f0xcrtiaicvmDFXwG2YmZqug/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



如果选择左外部： 

![img](https://mmbiz.qpic.cn/mmbiz_png/Ibz2ROUou9yvWGQGibgfnkEIGmAyQ19jRVOtic9AqT5GBwjJBibpkUuT70LTiaZDwvDkNJ7EaWk4D5QXFp4Gt7r1Ag/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



如果选择右外部： 

![img](https://mmbiz.qpic.cn/mmbiz_png/Ibz2ROUou9yvWGQGibgfnkEIGmAyQ19jRkTckBryFPY7eQhyicYBNZv7c6ibw8qBsrYW4cXZm05WXpsk71cMeTRYQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



如果选择完全外部： 

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)



如果选择内部： 

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)



如果选择左反： 

![img](https://mmbiz.qpic.cn/mmbiz_png/Ibz2ROUou9yvWGQGibgfnkEIGmAyQ19jROggZTLbibTg6Tr8G08ToA2HZJd7dF2a4PS234IzjJ0qKlmN5I6icFWhw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



如果选择右反： 

![img](https://mmbiz.qpic.cn/mmbiz_png/Ibz2ROUou9yvWGQGibgfnkEIGmAyQ19jRdW0gBZpJ7kmd06icniborttd9iaz63y3Pd5oOfYTHh3lmPhULfv0k1cZA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

总结：
左外部——保留表1 的所有项目，同时查询表2 和表1 的匹配项，排除表2 的不匹配项；
右外部——保留表2 的所有项目，同时查询表1 和表2 的匹配项，排除表1 的不匹配项；
完全外部——保留表1和表2 的所有项目；
内部——仅保留表1 和表2 的完全匹配项，排除其他项目；
左反——保留表1与表2 有差异的全部数据，排除表1 和表2 的匹配项；
右反——保留表2与表1有差异的全部数据，排除表2和表1 的匹配项。



好了，今天说了那么多，不知道你是听明白了，还是听糊涂了呢？



**PowerPivot工坊原创文章，转载请注明出处！*

------



Power Query M函数进阶课程，

即将上线，

敬请期待！



------



延伸阅读：

[Power Query数据处理躲坑系列一](http://mp.weixin.qq.com/s?__biz=MzI4NTEzNzQ2NQ==&mid=2650500934&idx=1&sn=ea75661395370a9fea99567bfb89cb4e&chksm=f3ff0010c48889061228a41e3c103ecf9dfc994bfa4c0581005b4fff7a965b4dce2e67905e7a&scene=21#wechat_redirect)

[Power Query数据处理躲坑系列二](http://mp.weixin.qq.com/s?__biz=MzI4NTEzNzQ2NQ==&mid=2650500957&idx=1&sn=341e5105eda18f7b4aa7e2186220f440&chksm=f3ff000bc488891d5a49221d22cc7a242ecd772e8d5df8e3afea49a3a2cb052483fdb786b790&scene=21#wechat_redirect)

[在Power Query中进行关键词匹配查询](http://mp.weixin.qq.com/s?__biz=MzI4NTEzNzQ2NQ==&mid=2650500644&idx=1&sn=725efa93a86d3b8f5f45db81d65453f4&chksm=f3ff0172c488886428c0f6d45b14e86caee252e7ef76746be4f0eb833477b68a39ecd6784c4b&scene=21#wechat_redirect)

[亮瞎双眼的Power BI可视化图表](http://mp.weixin.qq.com/s?__biz=MzI4NTEzNzQ2NQ==&mid=2650500487&idx=1&sn=78216bb746af5e401db30c64aa4b257c&chksm=f3ff02d1c4888bc755b0f81102574bc29062f9c989f7ae557ca344d90e259743cbf01b426333&scene=21#wechat_redirect)

[当Power BI遇上英雄联盟](http://mp.weixin.qq.com/s?__biz=MzI4NTEzNzQ2NQ==&mid=2650501408&idx=1&sn=9b888e61c6d643ee8eb5a59e8fbaccde&chksm=f3ff1e76c488976020a45c49a9346224997ccaab28d301172a2b8e375257fb04538f9ca8323d&scene=21#wechat_redirect)

[当Power BI 遇上洪灾](http://mp.weixin.qq.com/s?__biz=MzI4NTEzNzQ2NQ==&mid=2650501274&idx=1&sn=b759a4986531c4e3b67c4a511c9b0c48&chksm=f3ff1fccc48896dade617dedc52b31e3bf5927e14930227c8dd857b6fafb23441f08f5af1cc3&scene=21#wechat_redirect)

[当Power BI 遇上Visio](http://mp.weixin.qq.com/s?__biz=MzI4NTEzNzQ2NQ==&mid=2650501103&idx=1&sn=6ab4e768862446687b44a1c201d7b4ab&chksm=f3ff00b9c48889afafb6ba7f9eb843bcf405425f15df02f3d2da3678f3a9ab3be0245af46de8&scene=21#wechat_redirect)

[当Power BI 遇上欧冠决赛](http://mp.weixin.qq.com/s?__biz=MzI4NTEzNzQ2NQ==&mid=2650501040&idx=1&sn=b5502471009e33c8dafc5c9c2c4840f6&chksm=f3ff00e6c48889f0c1c677a1e506d0b5e5b9ed05f8cb7e24b7dfb79efb2e7dc04e561918bff1&scene=21#wechat_redirect)

[当Power BI遇上条形码](http://mp.weixin.qq.com/s?__biz=MzI4NTEzNzQ2NQ==&mid=2650500919&idx=1&sn=ad9fb69c94790427deb067cea355c267&chksm=f3ff0061c4888977bb29da066620b7d4fcf943f032563a468975dc2c712798c8c25bdd54615f&scene=21#wechat_redirect)

[当PowerBI遇上恐怖主义](http://mp.weixin.qq.com/s?__biz=MzI4NTEzNzQ2NQ==&mid=2650500271&idx=1&sn=d6f2817728a94decb30df9fc98f8e647&chksm=f3ff03f9c4888aefc792f25bff2f01e9ef341b99f123893f0d48d627ce47db1173dacb83094c&scene=21#wechat_redirect)

[一张图看懂微软Power BI 系列组件](http://mp.weixin.qq.com/s?__biz=MzI4NTEzNzQ2NQ==&mid=2650500496&idx=1&sn=5fd79724351c5febdd7ede92268ac2a7&chksm=f3ff02c6c4888bd08693dc85310f30879223b0adf99ef0d237b739a318abbdca549be26c91ba&scene=21#wechat_redirect)

[一张图看懂Power BI 架构](http://mp.weixin.qq.com/s?__biz=MzI4NTEzNzQ2NQ==&mid=2650501079&idx=1&sn=dcd2097539155b6cb56a811a8cdb04b5&chksm=f3ff0081c488899753cba20a60c10f17568b959745632e6d5807fb6ceefe7a472826cd24b1fc&scene=21#wechat_redirect)



------

如果您想深入学习微软Power BI，欢迎登录网易云课堂试听学习我们的“**从Excel到Power BI数据分析可视化**”系列课程。点击左下角“阅读原文”可直达云课堂。或者关注我们的公众号（PowerPivot工坊）后猛戳”在线学习”        

![img](https://mmbiz.qpic.cn/mmbiz/Ibz2ROUou9wjPm66fXjNOLCkCIxP04Rj6XEE5YuPC5Y6iccJ5vUBpFGjDEQG5afC2ZicicZcM75ic1H4aDsicoDkphw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

 

------

长按下方二维码关注“Power Pivot工坊”获取更多微软Power BI、PowerPivot相关文章、资讯。欢迎小伙伴儿们转发分享~ 

![img](https://mmbiz.qpic.cn/mmbiz/Ibz2ROUou9zPtXdA9jHQiaZkeic9yuMDUkoAUoYxbFKLgic4dO7oD8wjjYeicy84ziaIjJ5XqAR2tcPLvlb1BO7YuxQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)




  