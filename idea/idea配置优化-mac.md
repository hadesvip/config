```java
# custom IntelliJ IDEA VM options

##################JVM模式############################

# IDEA的JVM以Server模式启动（新生代默认使用ParNew）
-server

##################内存分配############################

# 堆初始值占用
-Xms2048m

# 堆最大值占用
-Xmx3500m

# Metaspace 空间大小
-XX:MaxMetaspaceSize=512m
-XX:MetaspaceSize=128m

# 强制JVM在启动时申请到足够的堆内存（否则IDEA启动时堆初始大小不足3g）
# -XX:+AlwaysPreTouch

# 年轻代与老年代比例为1:3（默认值是1:4），降低年轻代的回收频率
-XX:NewRatio=3

# 每个线程堆栈的大小 2m
# -Xss2m

##################老年代回收器############################

# 使用CMS老年代回收器
# -XX:+UseConcMarkSweepGC
# CMS的重新标记步骤：多线程一起执行
# -XX:+CMSParallelRemarkEnabled

#  使用 G1 (Garbage First) 垃圾收集器 （因为本地是JDK版本是JDK8，所以启用G1收集器，8以下的可以试用CMS收集器）
-XX:+UseG1GC


# 设置垃圾收集器在并行阶段使用的线程数[一般设置为本机CPU线程数相等，即本机同时可以处理的个数，设置过大也没有用]
-XX:ParallelGCThreads=4
# 并发垃圾收集器使用的线程数量 启用4个线程并发标记（理论上越多越好，前提是CPU核心足够多）
-XX:ConcGCThreads=2

##################JIT编译器############################
# 代码缓存，用于存放Just In Time编译后的本地代码，如果塞满，JVM将只解释执行，不再编译native代码。
-XX:ReservedCodeCacheSize=512m

# 分层编译，JIT编译优化越来越好，IDEA运行时间越久越快
-XX:+TieredCompilation

# 节省64位指针占用的空间，代价是JVM额外开销
#  -XX:+UseCompressedOops

# 增大软引用在JVM中的存活时长（堆空闲空间越大越久）
-XX:SoftRefLRUPolicyMSPerMB=50
-Dsun.io.useCanonCaches=false
-Djava.net.preferIPv4Stack=true
# -Djsse.enableSNIExtension=false

##################日志############################
# 禁止在启动期间显式调用System.gc()
-XX:+DisableExplicitGC

# 字体
-Dawt.useSystemAAFontSettings=lcd

# 关闭 fast throw 优化
-XX:-OmitStackTraceInFastThrow
-XX:ErrorFile=$USER_HOME/java_error_in_idea_%p.log

# 当堆内存空间溢出时输出堆的内存快照
-XX:+HeapDumpOnOutOfMemoryError
-XX:HeapDumpPath=$USER_HOME/java_error_in_idea.hprof
# 打印GC详细信息
-XX:+PrintGCDetails
# 打印CG发生的时间戳
-XX:+PrintGCTimeStamps
# 每一次GC前和GC后，都打印堆信息
-XX:+PrintHeapAtGC

-Xbootclasspath/a:../lib/boot.jar
-Dfile.encoding=UTF-8

-XX:MaxInlineLevel=3

##################其他设置############################
# 启动断言
-ea

-Dsun.java2d.renderer=sun.java2d.marlin.MarlinRenderingEngine
# 去除字节码验证
-Xverify:none
```

