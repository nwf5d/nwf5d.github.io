---
layout: post
title: 定时清除Zookeeper日志【转】
categories:
- Technology
tags:
- zookeeper
---

# 命令格式：

java -cp zookeeper.jar:log4j.jar:conf org.apache.zookeeper.server.PurgeTxnLog <dataDir> <snapDir> -n <count> 

举例：

java -cp zookeeper.jar:log4j.jar:conf org.apache.zookeeper.server.PurgeTxnLog /log/xres/zookeeper/zk_trlog /www/xres/app/zk_data -n 10 

定时清除zookeeper日志和快照数据非常简单，只需简单3步。

Step1：在zookeeper/bin目录建立purgeTxnLog.sh文件，内容如下所示：
