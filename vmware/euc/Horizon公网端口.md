# 组件
|**组件**|**描述**|**vCPU**|**内存/GB**|**存储/GB**|**数量**|**备注**|
| ----- | ----- | ----- | ----- | ----- | ----- | ----- |
|Connection Server|1.云桌面管理控制台<br>2.内网连接服务器|4|10|100|2| |
|App Volumes Manager|1.用户Profile+用户安装应用持久化可写卷<br>2.App Stack应快速推送|4|10|100|2| |
|MSSQL|日志数据库|4|8|100|2|Always On|
|UAG|1\. 公网安全接入网关<br>2\. 内网安全接入网关|2|4|50|2|VRRP|
|File Server|文件共享服务器，模拟NAS|4|8|500|1| |



# 防火墙放行端口
|**连接服务器放行端口**| | | | |
| ----- | ----- | ----- | ----- | ----- |
|**Port **|**Protocol **|**Source **|**Target**|**描述**|
|443 |TCP |Internet |UAG|Web traffic, Horizon Client XML - API, Horizon Tunnel,  Blast Extreme |
|443 |UDP |Internet |UAG|在UAG内部，UDP443端口会被转发到隧道服务器的UDP 9443端口|
|8443 |UDP |Internet |UAG|Blast Extreme (可选) |
|8443 |TCP |Internet |UAG|Blast Extreme (可选) |
|4172 |TCP/ UDP |Internet |UAG|PCoIP (可选) |
|443 |TCP |UAG|VCS|Horizon Client XML-API, Blast extreme HTML access, Horizon Air Console Access (HACA) |
|22443|TCP/ UDP |UAG|桌面/RDS |Blast Extreme 协议|
|4172 |TCP/ UDP |UAG|桌面/RDS |PCoIP (可选) |
|32111|TCP |UAG|桌面/RDS |USB Redirection 框架通道|
|9427 |TCP |UAG|桌面/RDS |MMR （多媒体重定向）and CDR （客户端驱动器重定向）|
|22443|TCP/ UDP |*VCS*|桌面/RDS |Blast Extreme 协议|
|4172 |TCP/ UDP |*VCS*|桌面/RDS |PCoIP (可选) |
|32111|TCP |*VCS*|桌面/RDS |USB Redirection 框架通道|
|9427 |TCP |*VCS*|桌面/RDS |MMR （多媒体重定向）and CDR （客户端驱动器重定向）|
|**管理放行端口**| | | | |
|**Port **|**Protocol **|**Source **|**Target **|**Description**|
|9443 |TCP |内网Admin网段|UAG|UAG管理接口|

 

注意：不建议生产中将VCS直接发布到公网。

如果为了PoC简化测试，直接发布VCS到公网，需要注意对VCS 8443端口做双向NAT，也叫U-Turn NAT或者叫做发夹NAT/回环NAT。

