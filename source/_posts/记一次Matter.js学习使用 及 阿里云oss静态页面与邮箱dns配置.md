---
layout: blog
title: 记一次Matter.js学习使用 及 阿里云oss静态页面与邮箱dns配置
date: 2021-02-07 
tags: 
- matter.js 
- aliyun
---
## 物理模拟  
鼠标在浏览器窗口里按下，即可生成一个小球。 快速移动并松开鼠标可将小球甩出。 小球符合自由落体规则，遇到窗口左、右、底部边界会反弹。 点击多次会生成多个小球。 


{% codepen xzifan RwoaYOo dark js 800px 800px %} 

## 阿里云oss静态页面与邮箱dns配置
1. 域名服务器需要设置为阿里云默认dns服务器，   
2. 在oss bucket 基础设置中设置首页和404页
3. 为邮箱和静态页面添加域名解析记录：  
<table>
    <tr>
        <td>主机记录</td>
        <td>记录类型</td>
        <td>解析线路</td>
        <td>记录值</td>
        <td>TTL</td>
    </tr>
    <tr>
        <td>@</td>
        <td>CNAME</td>
        <td>默认</td>
        <td>Bucket地址，如 xxx.oss-cn-xxx.aliyuncs.com</td>
        <td>10分钟</td>
        <td></td>
    </tr>
    <tr>
        <td>mail</td>
        <td>CNAME</td>
        <td>默认</td>
        <td>邮箱服务器,如 mail.mxhichina.com</td>
        <td>10分钟</td>
        <td></td>
    </tr>
    <tr>
        <td>smtp</td>
        <td>CNAME</td>
        <td>默认</td>
        <td>对应smtp, smtp.mxhichina.com</td>
        <td>10分钟</td>
        <td></td>
    </tr>
    <tr>
        <td>pop3</td>
        <td>CNAME</td>
        <td>默认</td>
        <td>对应pop3, pop3.mxhichina.com</td>
        <td>10分钟</td>
        <td></td>
    </tr>
    <tr>
        <td>@</td>
        <td>MX</td>
        <td>默认</td>
        <td>对应优先MX, mxn.mxhichina.com | 5 (mx优先级)</td>
        <td>10分钟</td>
    </tr>
    <tr>
        <td>@</td>
        <td>MX</td>
        <td>默认</td>
        <td>对应MX, mxw.mxhichina.com | 10 (mx优先级)</td>
        <td>10分钟</td>
    </tr>
</table>


    MX优先级，用来指定邮件服务器接收邮件的先后顺序，数值越小优先级越高。

    当DNS服务器的解析记录中只有一条MX记录时，MX优先级没有意义。
    当DNS服务器的解析记录中存在多条MX记录时，邮件发送方的DNS服务器会优先把邮件投递到MX优先级高的邮件服务器。
    如果该服务器故障无法接收邮件，邮件发送方的DNS服务器会自动选择下一优先级的邮件服务器投递邮件。

### 参考资料:  
- [Introduction to Matter.js - The Nature of Code](https://www.youtube.com/watch?v=urR596FsU68&ab_channel=TheCodingTrain)  
- [BRM.IO](https://brm.io/matter-js/)
- [MX优先级有什么意义？](https://support.huaweicloud.com/dns_faq/dns_faq_014.html)