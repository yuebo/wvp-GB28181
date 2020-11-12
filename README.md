# wvp
WEB VIDEO PLATFORM是一个基于GB28181-2016标准实现的网络视频平台，负责实现核心信令与设备管理后台部分，支持NAT穿透，支持海康、大华、宇视等品牌的IPC、NVR、DVR接入。   
流媒体服务基于ZLMediaKit-https://github.com/xiongziliang/ZLMediaKit
前段页面基于MediaServerUI进行修改.

本版本修改了INVITE部分，相关资料参考[https://www.cnblogs.com/dpf-10/p/8915723.html](https://www.cnblogs.com/dpf-10/p/8915723.html)

# 应用场景：
支持摄像机、平台、NVR等设备接入.
# 项目目标
旨在打造一个易配置,易使用,便于维护的28181国标信令系统, 依托优秀的开源流媒体服务框架ZLMediaKit, 实现一个完整易用GB28181平台. 

# 截图
![build_1.png](https://github.com/648540858/wiki/blob/master/images/Screenshot_1.png)
![build_1.png](https://github.com/648540858/wiki/blob/master/images/Screenshot_2.png)
![build_1.png](https://github.com/648540858/wiki/blob/master/images/Screenshot_20201012_151459.png)
![build_1.png](https://github.com/648540858/wiki/blob/master/images/Screenshot_20201012_152643.png)
![build_1.png](https://github.com/648540858/wiki/blob/master/images/Screenshot_20201012_151606.png)

# 原版特性：
1. 视频预览;  
2. 云台控制（方向、缩放控制）;  
3. 视频设备信息同步;   
4. 离在线监控;  
5. 录像查询与回放（基于NVR\DVR，暂不支持快进、seek操作）;  
6. 无人观看自动断流;    
7. 支持UDP和TCP两种国标信令传输模式;  

# 新支持特性  
1. 集成web界面, 不需要单独部署前端服务, 直接利用wvp内置文件服务部署, 随wvp一起部署;   
2. 支持平台接入, 针对大平台大量设备的情况进行优化;  
3. 支持检索,通道筛选;  
4. 支持自动配置ZLM媒体服务, 减少因配置问题所出现的问题;  
5. 支持启用udp多端口模式, 提高udp模式下媒体传输性能;  
6. 支持通道是否含有音频的设置;  
7. 支持通道子目录查询;  
8. 支持udp/tcp国标流传输模式;  
9. 支持直接输出RTSP、RTMP、HTTP-FLV、Websocket-FLV、HLS多种协议流地址  
10. 支持国标网络校时  
11. 支持公网部署, 支持wvp与zlm分开部署   

# 待实现： 
上级级联  
推流列表  
拉流列表  
web界面系统设置
使用mysql作为数据库  

# 项目部署
参考:[编译运行](https://github.com/648540858/wvp-GB28181/wiki/%E7%BC%96%E8%AF%91%E8%BF%90%E8%A1%8C)

# 使用帮助
QQ群: 901799015

# 致谢
感谢作者[夏楚](https://github.com/xiongziliang) 提供这么棒的开源流媒体服务框架  


# 项目调式相关

## 使用docker部署ZLMediaKit
```bash
docker run -id --net host --name media panjjo/zlmediakit
```
注意要使用--net=host参数，因为码流上传的时候端口是动态的。

## 修改相关配置

```bash
spring:
  redis:
    host: 192.168.7.93 # Redis服务器IP
sip:
  ip: 192.168.8.192
media: #zlm服务器的ip与http端口, 重点: 这是http端口
  ip: 192.168.7.202 #ZLMediaKit的IP
```
## 下周EasyGBD进行调试
如果当前没有设备，可以使用[EasyGBD](http://app.tsingsee.com/easygbd)来模拟，安装后填写:
1. SIP服务器地址为上面的sip.ip相同的值
2. SIP服务器端口填写为sip.port相同的值
3. SIP用户名和SIP用户认证ID填写为自己设备的编码，如34020000001320000099
4. SIP用户认证密码填写为12345678
5. 点击注册等待注册成功
6. 访问[sip服务器](http://localhost:18080)，用admin/admin登录，登录后便可以进行直播了。
