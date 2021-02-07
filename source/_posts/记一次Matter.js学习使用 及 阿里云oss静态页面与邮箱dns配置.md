---
layout: blog
title: 记一次Matter.js学习使用 及 阿里云oss静态页面与邮箱dns配置
date: 2021-02-07 
tags:
---
## 物理模拟  
鼠标在浏览器窗口里按下，即可生成一个小球。 快速移动并松开鼠标可将小球甩出。 小球符合自由落体规则，遇到窗口左、右、底部边界会反弹。 点击多次会生成多个小球。 

{% codepen xzifan RwoaYOo dark js 800px 800px %} 

## 阿里云oss
域名服务器需要设置为阿里云默认dns服务器，  
同时添加域名解析记录：  
主机记录 | 记录类型 | 解析线路 | 记录值 | TTL  
--- | --- | --- |--- |--- 
@ | CNAME | 默认 | xxx.oss-cn-xxx.aliyuncs.com | 10分钟  
mail | CNAME| 默认 | 邮箱服务器,如mail.mxhichina.com | 10分钟  
smtp | CNAME| 默认 | 对应smtp, smtp.mxhichina.com | 10分钟  
pop3 | CNAME| 默认 | 对应pop3, pop3.mxhichina.com | 10分钟  
@	| MX	| 默认 | 对应优先MX, mxn.mxhichina.com \| 5 (mx优先级) | 10分钟
@	| MX	| 默认 | 对应MX, mxw.mxhichina.com \| 10 (mx优先级) | 10分钟
### 参考资料:  
[Introduction to Matter.js - The Nature of Code](https://www.youtube.com/watch?v=urR596FsU68&ab_channel=TheCodingTrain)
[BRM.IO](https://brm.io/matter-js/)