# Crack Skid Client

所有类名会将 invalid char 忽略

基于 forge 获取的 melon_class_hierarchy.txt

可以大致发现两个后门

均为 skid  (一个从ccc, 一个 discord token logger)

## 后门查找

### ccc 后门

com/qqTechnologies/qqbackdoor/Bootstrapper

com/qqTechnologies/qqbackdoor/MainClass

### discord token logger 

jibet/zenhao/melon/util/token/ 下左右class

## 逆向 Jar

#### 删除后门

基于原始类结构

CNM / NMSL / 6YM / IS / GAY 即有可能为 eskid 生成的 trash classes

### ccc  后门

根据原始后门 (ccc) 的源码, 逆向查找 sendJar( bytearray, str )V; 的 method, 并找到类

melon / 0 / melon / 0

melon / 0 / melon / c

删除即可。

##### discord token logger

由于类比较多

可以根据特殊标志, 在这里, 则是 gson 的 序列化注解

使用recaf查找特征

melon / 0d ( 不包含 melon / 0d / melon  )

melon / 0l

melon / P / melon / d

删除即可

## 删除验证

由于 zenhao 太菜, 并且 melon 为 kami skid, 所以跟 uwugod 一样. 

遍历 class 内有两个返回 boolean 的 method, 并且调用 JOptionPane.showMessageDialog

便可找到 

melon / 0g / melon / 9

其中 awa() 以及 owo() 变为验证, 与 uwugod 基本一致

在 idea 中, 使用 debugger 断点，便可查找到 url 验证的网站

https://pastebin.com/gr8xLash

### 更改字节码

[图片1](1.png)

1. 首先在 recaf 中将 类模式 改为 Table

[图片2](2.png)

2. 选中 方法 一栏

[图片3](3.png)

3. 右键 awa 一行, 单击 编辑汇编代码

[图片4](4.png)

4. 除了第一行 DEFINE 开头, 删除全部

5. 输入以下两行

	ICONST_1
	IRETURN

6. 按 Ctrl + S 保存

[图片5](5.png)

7. owo 同理

#### 字节码解析

ICONST_1

Int 1, 也就是 true

IRETURN

返回

相当于把整个方法删除, 替换为 return true;

你就破解完成了, 恭喜, 可以耀武扬威去了

## 修复 Jar

由于删除了一些后门的 class, 运行时有可能会报错, ClassNotFoundError

请根据 stacktrace 找到调用处

recaf 里删除相关调用代码即可, 注意保持 jvm stack ! recaf 的 stack 工具可以很好的帮助你



## 其他

当然，你也可以通过更换 url 来完成自己的验证



# Credits

Han: for finding out the backdoor

Zenhao: for writing such a bad client

Killred: Thank God eskid is not that good in this case

Col-E: recaf is cool

blablabla I can't think more.







