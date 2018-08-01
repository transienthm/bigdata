# 一、Hadoop

## 1.1 Hadoop背景

![image](https://user-images.githubusercontent.com/16509581/43432382-256ec7ee-94a5-11e8-89e8-e24a6f3b7150.png)

![image](https://user-images.githubusercontent.com/16509581/43432389-3080e1a8-94a5-11e8-8737-e2542c9db0d2.png)

![image](https://user-images.githubusercontent.com/16509581/43432410-5b0b10ce-94a5-11e8-8ef7-8def0bff0b46.png)

![image-20180731094933533](/var/folders/dq/bwscczgs1m10n6c_4b1hg3m40000gp/T/abnerworks.Typora/image-20180731094933533.png)

![image-20180731095117838](/var/folders/dq/bwscczgs1m10n6c_4b1hg3m40000gp/T/abnerworks.Typora/image-20180731095117838.png)

红色为Hadoop的子项目。

## 1.2 HDFS

### 1.2.1 HDFS基本情况

![image](https://user-images.githubusercontent.com/16509581/43445905-15037d48-94da-11e8-8525-bf6646ed4815.png)![image](https://user-images.githubusercontent.com/16509581/43445996-437dc390-94da-11e8-9c92-17bdb694bbcd.png)

![image](https://user-images.githubusercontent.com/16509581/43446026-5a386b76-94da-11e8-9971-d04375a012c6.png)

支持shell命令

![image](https://user-images.githubusercontent.com/16509581/43446101-9c7a0cce-94da-11e8-8502-79d831296dc6.png)

![image](https://user-images.githubusercontent.com/16509581/43446275-00d6105a-94db-11e8-9092-2d2fc62197e5.png)

![image](https://user-images.githubusercontent.com/16509581/43446317-1ba5b052-94db-11e8-9b5c-0d3d46c28a65.png)



### 1.2.2 HDFS架构及设计思想

![image](https://user-images.githubusercontent.com/16509581/43449487-245de27a-94e3-11e8-885c-1c682276d5e0.png)

HDFS Client请求NameNode



![image](https://user-images.githubusercontent.com/16509581/43449762-dce78c42-94e3-11e8-925b-fc68dcdf0553.png)



一个块存储一个文件的信息。一个块只是一个逻辑结构，并非占满64M的空间

![image](https://user-images.githubusercontent.com/16509581/43452225-827bef72-94e9-11e8-8973-7a66636eaab6.png)

### 1.2.3 结点介绍（NN、SNN、DN）

![image](https://user-images.githubusercontent.com/16509581/43452246-9471616c-94e9-11e8-874c-3e01383060df.png)

![image-20180731175311024](/var/folders/dq/bwscczgs1m10n6c_4b1hg3m40000gp/T/abnerworks.Typora/image-20180731175311024.png)

![image](https://user-images.githubusercontent.com/16509581/43453922-ffec43d6-94ed-11e8-9532-60ca477e50d8.png)

![image](https://user-images.githubusercontent.com/16509581/43453943-0cd30b70-94ee-11e8-9049-00bad27f774a.png)

![image](https://user-images.githubusercontent.com/16509581/43454233-f7c10c72-94ee-11e8-87a0-d7e248fe4a55.png)

### 1.2.4 读写、权限及安全模式

![image](https://user-images.githubusercontent.com/16509581/43454722-7f5d2e4e-94f0-11e8-995f-63615723f5f2.png)

1. client 发送读请求
2. 使用 NameNode 的 Api 获得 block 的位置
3. 通过 FSDataInputStream 的流并发读取各个 block （图中4 5表示并发读取）
4. 关闭流

![image](https://user-images.githubusercontent.com/16509581/43455586-f0c276d2-94f2-11e8-8028-0a7a4206eac0.png)

1. client 调用 DistributedFileSystem 的 create Api可以创建一个文件
2. 请求 NameNode 得到需要切成多少个block的信息，以及分别存储在哪些DataNode上
3. 通过 FSDataOutputStream 创建写入流
4. 向其中一个 DataNode执行写入操作，再由该DataNode创建线程，向其他DataNode 复制复本
5. 完成后返回确认信息
6. 关闭流
7. 回馈信息给NameNode

![image](https://user-images.githubusercontent.com/16509581/43455999-61011b82-94f4-11e8-8601-b2e959817738.png)

![image](https://user-images.githubusercontent.com/16509581/43456113-cc02dc2c-94f4-11e8-9190-2d2d7f102895.png)

### 1.2.5 HDFS的安装

