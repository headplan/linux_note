# oauth-php

http:\/\/code.google.com\/p\/oauth-php\/

### 项目主页介绍

OAuth Consumer And Server Library For PHP.它包含一个完整实现的可扩展的OAuth存储,支持MySQL\/MySQLi,Postgresql,PDO和Oracle等多种存储方式.

它实现了以下方法:

* 认证进来的请求
* 为出去的请求签名
* 使用 body 为请求签名
* 为多用户管理消费方的 key 和 token（服务端和消费端）
* 记录经过类库处理的进出的请求（可以在数据库中进行可选配置）

为服务器增加OAuth,需要检查进来的请求中OAuth认证细节.首先,我们需要4个控制器:

* oauth\_register.php - 使消费方用户获得 key 和密钥
* request\_token.php - 返回一个未认证的 request token
* authorize.php - 认证一个request token
* access\_token.php - 将认证后的 request token 置换为 access token

