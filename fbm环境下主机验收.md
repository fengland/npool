<center><h1>FBM环境下验收</h1></center>

# 注意：不要对已交付的机器进行验收

# 1、fbm环境准备

设置工作目录

```bash
root@test:/opt/fbm# export LOTUS_WORKSPACE=$PWD/../src
```

准备相关工具及主机清单目录

```bash
root@test:/opt/fbm# ./utils/ep -c prepare
```

\#创建验收使用的主机清单

拷贝主机清单

```bash
root@test:/opt/inventory/test-inventory#cp [主机清单名字] [机房名字-客户名字]-machchk
```

建议命名 [机房名]-[客户名]-[machchk],如 nm-anson-1-machchk

# 2、建议开两个窗口

```bash
root@test:~# cd /opt/fbm/  #第一窗口进入
root@test:/opt/fbm#      #目录下执行行命令
root@test:~# cd /opt/inventory/test-inventory/   #第二窗口进入
root@test:/opt/inventory/test-inventory# ls    #目录下编辑主机清单
jh-huoxing-machchk  machchk-template template XJP-dalu-work
jh-onetiger-machchk README.md     XJP-dalu
```

## **第一步编辑主机清单**

```bash
cd /opt/inventory/test-inventory
```

```bash
ls 看下有没有自己的主机清单
root@test:~# cd /opt/inventory/test-inventory/   #进入主机清单所在目录
root@test:/opt/inventory/test-inventory# ls  #看下有没有自己的主机清单
jh-huoxing-machchk  machchk-template template XJP-dalu-work
jh-onetiger-machchk README.md     XJP-dalu
root@test:/opt/inventory/test-inventory# vi jh-huoxing-machchk
```

![image-20220527151121087](C:\Users\wangxufeng\AppData\Roaming\Typora\typora-user-images\image-20220527151121087.png)

 

<img src="C:\Users\wangxufeng\AppData\Roaming\Typora\typora-user-images\image-20220427233537162.png" alt="image-20220427233537162" style="zoom:200%;" />

# 3、miner/worker验收流程

## 一、编辑 Miner / Worker 验收使用的主机清单 Miner 验收指标参考

·     vi \$LOTUS_WORKSPACE/test-inventory/$clustername

·     修改集群名称 clustername 替换为$clustername

·     修改 myip myip 替换为$myip

·     添加 Miner 验收指标

·     添加工人验收指标

添加 checknetnode，用于网络测试

## 二、miner/worker硬件验收（cd  /opt/fbm目录下执行）

1、确认所填写的机器列表在线 ping在线主机

```bash
root@test:/opt/fbm# ./command/ping -d /opt/fbm -l 主机清单名称  
```

结果无报错，全部设备在线

2、执行硬件验收（重置重启机器后执行）

```bash
root@test:/opt/fbm# ./command/machineacceptance -d /opt/fbm/ -l 主机清单名称
```

3、执行硬件验收（加** **-R****，不重启机器）

```bash
root@test:/opt/fbm# ./command/machineacceptance -d /opt/fbm/ -l 清单 -R
```

4、查看硬件验收结果

```bash
root@test:/opt/fbm# vi output/主机清单名称/machchk/ all.machine.report.abs
root@test:/opt/fbm#grep ERROR output/主机清单名称/machchk/all.machine.report.abs
```

2.5、网络基准测试

```bash
root@test:/opt/fbm# ./command/publicnettest -d /opt/fbm/ -l 主机清单名称
```

查看网络基准测试结果

```bash
root@test:/opt/fbm#vi output/主机清单名称/publicnettest/public-iperf-128K.csv
root@test:/opt/fbm#vi output/主机清单名称/publicnettest/public-ping.csv
```

2.6、磁盘基准测试

```bash
root@test:/opt/fbm#./command/basedisktest -d /opt/fbm / -l 主机清单名称
```

查看磁盘基本测试结果

```bash
root@test:/opt/fbm#vi output/主机清单名称/basedisktest/fio-result.csv
root@test:/opt/fbm#vi output/主机清单名称/basedisktest/all.basedisktestresult.abs
root@test:/opt/fbm#grep ERROR output/主机清单名称/basedisktest/all.basedisktestresult.abs
```

# 4、存储机验收流程

## **一、整合存储机测试结果及硬件信息**

**整合获取硬件信息**

```bash
root@test:/opt/fbm#./command/machineinfo -d /opt/fbm/ -l 主机清单名称
root@test:/opt/fbm#vi output/主机清单名称/machineinfo/results/check_cpu_results.csv
root@test:/opt/fbm#vi output/主机清单名称/machineinfo/results/check_disk_results.csv
root@test:/opt/fbm#vi output/主机清单名称/machineinfo/results/check_mem_results.csv
root@test:/opt/fbm#vi output/主机清单名称/machineinfo/results/check_net_results.csv
root@test:/opt/fbm#vi output/主机清单名称/machineinfo/results/check_os_results.csv
```

**测试文件结果下载**

```bash
root@test:/opt/fbm/output# sz jh-huoxing-machchk/fio/172.19.17.51.fio
```

 

 

 

