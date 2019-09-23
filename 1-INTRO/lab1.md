# <center>实验报告</center>  
### <center>实验一 入门</center>  
### <center>Lab1 INTRO</center>  
##### <p align="right">罗晏宸</br>PB17000297</br>2019.9.7</p>
***
## 实验目的
1. **入门Wireshark**  
    熟悉Wireshark软件界面、功能，学习基本的分组捕获与分析方法，尝试阅读网络信息  

***
## 实验内容  
### 1. 列举捕获的分组中若干不同的网络协议

​	**NBNS**, **DNS**, **UDP**, **SSL**, **SSDP**, **TCP**, **HTTP**, **WebSocket**, **TLSv1.2**, **TLSv1.3**, **ARP**, **ICMPv6**, **LLMNR**, **MDNS**

### 2. 获取网络请求发出到接受的间隔时间

$$
23:06:25.295585-23:06:24.993846=0.301739 \mbox{s}
$$

### 3. 获取本机与目标站点的网络地址

- 目标站点 Host: pixel.fonexsoftware.com:1453

- 本机 Origin: chrome-extension://npmleadjnlojpinmkhnepddhlplealpg

### 4. 打印输出捕获结果

![打印输出](https://github.com/lyc0930/Wireshark-Labs/blob/master/Lab1-INTRO/Print.png?raw=true)  

## 实验截图

1. 软件界面  

    ![初始界面](https://github.com/lyc0930/Wireshark-Labs/blob/master/Lab1-INTRO/initial_interface.png?raw=true)  

2. 按协议过滤  
    ![按协议过滤](https://github.com/lyc0930/Wireshark-Labs/blob/master/Lab1-INTRO/filtered.png?raw=true)  

3. 查看分组细节  
    ![最大化细节](https://github.com/lyc0930/Wireshark-Labs/blob/master/Lab1-INTRO/Maximized.png?raw=true)  

4. 查看请求与接受间隔  
    ![分组时间](https://github.com/lyc0930/Wireshark-Labs/blob/master/Lab1-INTRO/time.png?raw=true)

    ![分组时间间隔](https://github.com/lyc0930/Wireshark-Labs/blob/master/Lab1-INTRO/time2.png?raw=true)  

## 实验总结

<p>作为本学期计算机网络课程的第一次观察实验，通过对于Wireshark软件的尝试与摸索，掌握了其基本功能及部分使用方法，包括捕获分组、查看分组头部细节、打印输出捕获结果等。进一步地，通过一个简单HTTP协议的例子，观察了实际分组的细节，回顾了已学习的相关知识。经过本次入门实验，引入了本学期观察实验的重要工具Wireshark，为今后的实验学习与实践提供了背景与工具。</p>  
## 附
本报告中出现的所有设计与测试源代码文件以及相关截图与照片可见[GitHub@lyc0930](https://github.com/lyc0930/Wireshark-Labs)