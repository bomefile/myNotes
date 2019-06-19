
1. 安装
````
brew install httpd
````
2. 测试

````
wangliangliangdeMacBook-Pro:~ wangliangliang$ ab -n 4 -c 2 https://www.baidu.com/
This is ApacheBench, Version 2.3 <$Revision: 1843412 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking www.baidu.com (be patient).....done


Server Software:        BWS/1.1
Server Hostname:        www.baidu.com
Server Port:            443
SSL/TLS Protocol:       TLSv1.2,ECDHE-RSA-AES128-GCM-SHA256,2048,128
Server Temp Key:        ECDH P-256 256 bits
TLS Server Name:        www.baidu.com

Document Path:          /
Document Length:        227 bytes

Concurrency Level:      2
Time taken for tests:   0.118 seconds
Complete requests:      4
Failed requests:        0
Total transferred:      3572 bytes
HTML transferred:       908 bytes
Requests per second:    34.04 [#/sec] (mean)
Time per request:       58.752 [ms] (mean)
Time per request:       29.376 [ms] (mean, across all concurrent requests)
Transfer rate:          29.69 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       25   30   6.8     28      40
Processing:     6    9   2.1      9      11
Waiting:        6    9   1.9      9      10
Total:         34   39   6.9     38      49

Percentage of the requests served within a certain time (ms)
  50%     38
  66%     38
  75%     49
  80%     49
  90%     49
  95%     49
  98%     49
  99%     49
 100%     49 (longest request)
````