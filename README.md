# 实验目的
-  COM组件和调用
# 实验任务
- 构建一个com组件，该组件可以对一个字符串数组进行加密和解密；
# 环境设置、工具
- java jdk （1.6或者以上）
- IDEA 或者 eclipse 等开发环境
- Visual Studio 2015
- jacob-1.19
# 具体过程
### 1. Visual Studio平台C#写com组件
#####a.  新建->项目->Visual C#->选择【类库】,名称自定义：MyComToJava

![创建项目](https://i.loli.net/2019/06/21/5d0c5b86b2e8648918.jpg)


#####b.  重命名cs文件：MyComToJava.cs

![重命名cs文件](https://i.loli.net/2019/06/21/5d0c5bdb9b8fc49799.jpg)

#####c.  修改属性配置
右键点击工程->属性->应用程序->程序集信息->选中“使程序集COM可见（M）”

![修改配置1](https://i.loli.net/2019/06/21/5d0c5ca3c230742608.jpg
)

生成->“为COM互操作注册（C）”打上勾，保存

![修改配置2](https://i.loli.net/2019/06/21/5d0c5ca45c5c470502.jpg
)

签名->“为程序集签名（A）”打上勾->新建签名MyComToJava->取消勾选“使用密码保护密钥文件”

![修改配置3](https://i.loli.net/2019/06/21/5d0c5cfc576d942340.jpg
)

#####d.  通过点击工具->创建 GUID->选择5->新建 GUID->复制->替换C#代码中的两个 GUID 值

![GUID](https://i.loli.net/2019/06/21/5d0c5d55aafcc14279.jpg)

#####e.  编写ComToJava

![ComToJava](https://i.loli.net/2019/06/21/5d0c65537e62c99042.jpg
)

#####f.  编译生成解决方案，Debug目录中会生成MyComToJava.dll文件

![生成解决方案](https://i.loli.net/2019/06/21/5d0c5e20afbf280512.jpg
)
![MyComToJava.dll](https://i.loli.net/2019/06/21/5d0c5e20a485b86718.jpg
)

### 2. 注册COM组件至系统
开始菜单->打开VS 2015自带CMD命令窗口（管理员权限）->定位至MyComToJava.dll文件夹下  。
执行：gacutil /i MyComToJava.dll 添加dll至全局缓存 ；
执行：regasm MyComToJava.dll 注册dll至系统 。

![MyComToJava.dll](https://i.loli.net/2019/06/21/5d0c5f6d57b8571888.png)

查看注册表regedit,HKEY_CLASSES_ROOT中是否有MyComToJava.VerifyCode项。如果有，则说明注册COM成功；如果没有，请重新注册

![注册表](https://i.loli.net/2019/06/21/5d0c5fdd5f33c38123.jpg)

### 3. Java调用com
#####a.  IDEA新建Java项目：VerifyCodeComToJava
右键项目->点击“Open Module Settings”->选择【Modules】->在右侧的Dependencies中点击“+”，选择“JARs OR directories...”->选择jacob.jar所在文件夹

![jacob.jar](https://i.loli.net/2019/06/21/5d0c6119db11f45252.jpg)

#####b.  创建调用类

![调用类](https://i.loli.net/2019/06/21/5d0c661a603c267126.jpg)

### 4. 调用结果

![结果](https://i.loli.net/2019/06/21/5d0c666c2605626948.jpg)


