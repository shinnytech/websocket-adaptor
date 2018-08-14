# websocket-adaptor

本工具实现一个websocket接口到两个本地文件的互相转接, 包括:

- 与一个给定 URL 建立 websocket 连接
- 从指定的文件A(可以是stdin)中逐行读取文本, 每行文本形成一个websocket包, 发送到 websocket 连接
- 从websocket接口持续接收数据包, 输出到文件B, 每个数据包为一行

## 主要应用

本工具可用于简化各类程序实现websocket通讯的开发工作, 甚至对没有源代码的程序也可适用.

### 示例1: 将程序X的print输出转发到websocket端口

假定我们有某C++程序cprog.exe, 它定时通过print输出一些信息

```c
for (int i=0; i<100; i++){
    printf("{\"no\": %d}\n", i);
}
```

我们希望将它的输出信息直接发送到 ws://202.196.3.23:7890/a/b/c , 只需这样即可实现, 不用修改cprog的源码:

```
cprog.exe | python adaptor.py ws://202.196.3.23:7890/a/b/c
```
