### Radis未授权访问

https://blog.csdn.net/qq_26091745/article/details/117222362

[https://www.hacking8.com/bug-product/Redis/redis%E6%9C%AA%E6%8E%88%E6%9D%83%E8%AE%BF%E9%97%AE%E6%BC%8F%E6%B4%9E.html](https://www.hacking8.com/bug-product/Redis/redis未授权访问漏洞.html)



#### 环境准备

```plain
从官网wget到本地
wget http://download.redis.io/releases/redis-3.2.11.tar.gz 
tar xzf redis-3.2.11.tar.gz 
将redis.conf copy到 /etc/下
启动时使用命令 redis-server /etc/redis.conf
测试时建议 vim /etc/redis.conf
去掉ip绑定，允许除本地外的主机远程登录redis服务
(1)bind 127.0.0.1前面加上##号注释掉 或者更改成 0.0.0.0
(2)protected-mode设为no
```

#### 攻击常用命令

```
redis-cli -h  -p 6379	链接radis
info 查看信息
flushall 删除所有数据库内容
flushdb 刷新数据库
看所有键：KEYS *，使用select num可以查看键值数据
set test "who am i" 设置变量
config set dir dirpath 设置路径等配置
config get dir/dbfilename 获取路径及数据配置信息
save 保存
get	 变量，查看变量名称
```

#### msf常用攻击模块

```
auxiliary/scanner/redis/file_upload 
auxiliary/scanner/redis/redis_login 
auxiliary/scanner/redis/redis_server
```

#### radis服务发现

`nmap -A -p 6379 --script redis-info <ipAddr>`