# 一款基于命令行的压测小工具ApiPressure

+ 支持HTTP GET, POST, PUT, DELETE, HEAD操作
+ 支持长连接
+ 支持多个URL混合测试
+ 支持超时时间设置
+ 支持身份认证， Basic Auth和Digest Auth

### 安装：

```
pip install apipressure
```

### 命令行选项：

```shell
NikanMacBookPro:~ nikan$ apipressure
usage: apipressure [-h] [-c CONCURRENCY] [-n TOTAL_REQUESTS] [-m METHOD]
                   [-f FILE_PATH] [-d DATA] [-j JSON] [-t TIMEOUT] [-k]
                   [-a AUTH] [-H HEADERS] [-C COOKIES] [--version]
                   urls [urls ...]

HTTP压测小工具🎂 Author: kamalyes(mryu168@163.com)

positional arguments:
  urls                  请求URL(一个或多个)

optional arguments:
  -h, --help            show this help message and exit
  -c CONCURRENCY, --concurrency CONCURRENCY
                        并发数
  -n TOTAL_REQUESTS, --number TOTAL_REQUESTS
                        请求数
  -m METHOD, --method METHOD
                        请求方式{GET,POST,DELETE,PUT,HEAD,OPTIONS}
  -f FILE_PATH, --file FILE_PATH
                        文件路径
  -d DATA, --data DATA  post/put 数据
  -j JSON, --json JSON  post/put json 数据
  -t TIMEOUT, --timeout TIMEOUT
                        超时时间
  -k, --keep-alive      是否启用长连接
  -a AUTH, --auth AUTH  身份认证 eg. basic:user:password
  -H HEADERS, --headers HEADERS
                        请求头
  -C COOKIES, --cookies COOKIES
                        请求cookies
  --version             当前版本
```

### 例子:

```shell
# 对单个请求进行get测试
apipressure -c 10 -n 30 https://www.baidu.com
# 允许keep-alive
apipressure -k -c 10 -n 30 https://www.baidu.com
# 设置超时时间（整数）
apipressure -t 1 -c 10 -n 30 https://www.baidu.com
# 对多个URL进行混合请求
apipressure -c 10 -n 30 https://www.baidu.com http://example.com/ https://www.taobao.com/
# basic auth
apipressure -a basic:test_user:test_password http://example.com/
# digest auth
apipressure -a digest:test_user:test_passtest_password http://example.com/

# post json
apipressure -m POST -j "{'test':'test_json'}" -c 10 -n 100 http://example.com/ 

# post data
apipressure -m POST -d "{'test':'test_json'}" -c 10 -n 100 http://example.com/ 

# Headers和Cookies
apipressure -H "{'user-agent':'hahah'}" -C "{'a':'1'}" http://example.com/

# 有非常多的url可以放于文件中,每行一个url
apipressure -f benchamark.txt
```

输出示例：

```shell
NikanMacBookPro:~ nikan$ apipressure -c 10 -n 30 https://www.baidu.com
正在进行压测.....
压测结果========================
并发数：                10
请求数：                30
失败数：                0
非200请求数：           0
平均请求时长（秒）：    0.100
============================
请求时间分布（秒）
0%（最快）0.078
10%  0.080
50%  0.094
90%  0.118
95%  0.121
100%（最慢）0.183
```

