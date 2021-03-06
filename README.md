# FaceRecognizerServer
脸部识别的系统，用于校验输入人脸的身份。

# 历史版本
## 最初目的
初始版本由于在帮别人做一个手机 App 时对接服务属于内部网络，VPN 接入后又会带来其他问题，
为了调试方便，所以模拟服务实现接口。  

## 目前    
按照可以商用的目的，实现该有的接口服务，并且优化性能，当然过程中也会使用一些之前没有使用过的框架。

### 待优化的地方  
```
1.使用并发或者分布式的方式实现 image save
2.熟悉 dlib，解决图片加载或者保存的方式，优化服务启动速度
```

# 后续  
由于这几年本身的工作一直在 hyperledger fabric 上，今天大体考虑可以在这方面做点事情。
由于本人在人脸识别行业上没有实质的工作经验，对市场了解也不是很清楚。比如大部分商户在使用
人脸识别时可能并不会有用户信息共享的场景。

# 整体模型  
![image](https://raw.githubusercontent.com/KevinBaiSg/FaceAuthChain/master/images/FaceAuth.png)

# 1-N 匹配的查找设计模型  
![image](https://raw.githubusercontent.com/KevinBaiSg/FaceAuthChain/master/images/concurrency.png)  

### 大体想法
```
1.图像序列化能够存储到链上。
2.使用链上数据校验待验证的人脸图片。
3.验证过程由于使用到图像识别的技术，所以可以在服务中校验，区块链目的只是一个可信的数据库。
4.多个节点共享人脸数据，可以起到可信共享数据的作用，省去了重复注册。
5.可以利用 MSP 的特性，配置注册脸部数据时多个节点背书
```
# ref  
[Face recognition with Go](https://hackernoon.com/face-recognition-with-go-676a555b8a7e)  
[dlib Machine Learning Guide](http://dlib.net/ml_guide.svg)  

Descriptor -> [gob](https://golang.org/pkg/encoding/gob/#pkg-examples)序列化