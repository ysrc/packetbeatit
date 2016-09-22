[![Travis](https://travis-ci.org/elastic/beats.svg?branch=master)](https://travis-ci.org/elastic/beats)
[![AppVeyor](https://ci.appveyor.com/api/projects/status/p7y92i6pp2v7vnrd/branch/master?svg=true)](https://ci.appveyor.com/project/elastic-beats/beats/branch/master)
[![GoReportCard](http://goreportcard.com/badge/elastic/beats)](http://goreportcard.com/report/elastic/beats)
[![codecov.io](https://codecov.io/github/elastic/beats/coverage.svg?branch=master)](https://codecov.io/github/elastic/beats?branch=master)

# peacketbeat修改版 ，包含 beats 

## 1.编译方法 
添加 GOPATH到环境变量 

如 export GOPATH=/root/go ，可以把环境变量这个添加到.bashrc里 

在beats目录下make ，编译不过没事 。只要 libbeat编译通过就好 

到packetbeat目录编译 ，获得可执行文件 


## 2.默认配置

修改 peacketbeat.yml 


在#========================== Transaction protocols =============================段内添加：

packetbeat.protocols.http:

　　ports: [80, 8080, 8000, 5000, 8002]
   
　　split_cookie: true
   
   　　send_headers: ["User-Agent"]
   
   　　send_all_headers: true
   
   　　include_body_for: ['text','image','application']
   
   　　real_ip_header: 'X-Forwarded-For'
   
   　　send_request: true
   
   　　send_response: true
   
   　　transaction_timeout: 10
   
   　　specify_host: ["www.ly.com"]
   
　　specify_referer: ["www.ly.com"]
   
　　 redact_authorization: true
   
   
   
在#================================ Outputs =====================================段内添加 

output.console:

　　　pretty: true
       
       

## 3.启动命令 

1.修改配置文件 

2.检查配置文件正确性 ： ./packetbeat -configtest -e

3.启动： ./packetbeat -e -c packetbeat.yml



## 4.修改点

1.添加url过滤

2.添加host过滤

使用：在配置里加上specify_host和specify_referer把需要的host和refer加上，不加默认全部接收。
