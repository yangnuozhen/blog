# iOS运行Minecraft:Java服务端

>最开始发在[CSDN](https://blog.csdn.net/weixin_42718194/article/details/119607974)，图懒得重新搞了

## 写在前面

众所周知，iOS的封闭性不用多说，所以我们几乎不可能在iOS上运行java，更何况是Minecraft服务器。。。。。了吗？

错误的。相信深入了解过苹果设备的人都知道，有一个能够突♂破苹果重重封锁的东西，就叫做越狱。

相信你接触过越狱吧。什么？你没接触过？去搜索一下怎么越狱再回来看看这篇文章吧。

OK，你肯定已经做好了越狱的准备，那我们开始吧！

## 材料准备

 - 一台越狱后的iOS设备（此文使用的是iPhone7，iOS14.3，使用unc0ver越狱）
 - 一台电脑（可选）
 - 一堆插件（后文会提到）
 


## 一、环境准备

### 配置环境
>一般来说，越狱工具会自带软件包管理程式，譬如Cydia、Zebra，他们都是APT的GUI实现。你可以自己上网查询它们的使用方法。此处以Cydia为例。
>SSH在越狱环境中起着重要作用，iPhone中使用的ssh服务器一般是[Openssh](https://www.openssh.com/)。

#### 1.安装Opensssh

打开Cydia，如果你是第一次越狱，可能会出现无法联网等问题，建议自行查找解决方案，此处不多描述。


![Cydia首页](https://img-blog.csdnimg.cn/295d0db0e65d4ecfad4167381d18260c.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70#pic_center)

点击首页的OpenSSH访问教程

![qwq](https://img-blog.csdnimg.cn/ef15e869f0f64409ab61f2679e8f844d.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70#pic_center)
你会看到一堆英文。你或许看不懂，没关系跟我走就对了。看得懂也跟我走吧（

首先，你会在教程的页面中第一步里看到一个蓝色的“OpenSSH”，什么也不用管，点进去就好了。

于是，你进入到了OpenSSH的介绍网页。

点击在Cydia横幅上面的open按钮，

![](https://img-blog.csdnimg.cn/f993b8abb09c4c4bbd20120fa6bad994.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70#pic_center)
稍等片刻，你会进入到进入到软件包页面。

此时，右上角的`重新加载`会变成`安装`按钮。

点击右上角的安装按钮，然后在弹出的菜单内点击安装，在确认队列中选择右上角的确定，开始安装OpenSSH。

安装结束后看看黑框内的日志中是否有红字，如果没有，在页面底部会有一个按钮，点它就行了。

#### 2.添加软件源

在Cydia的底部，有一个叫做“软件源”的选项卡，点进去，然后先在右上角轻触“编辑”，然后再按下左上角的“添加”

![于是你得到了它](https://img-blog.csdnimg.cn/24fe802f1c764f67942b8ef4264f45f2.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70#pic_center)

然后在输入框中删除全部内容，然后输入


`https://doregon.github.io/cydia`

然后点击“添加源”，等待软件源刷新。刷新完毕后，你应该会在软件源列表中看见“Doregon's Repo”软件源。

---


#### 3.安装Java Runtime Environment

首先，在你刚才进入软件包所看到的分类中，选择“开发”分类。
然后，你会看到一些软件包。我们只需要带有“openJDK”的软件包。但是！请不要急着全部安装。
![openjdk软件包](https://img-blog.csdnimg.cn/4007d7f92efd42e7ad8bb07eccd1e43b.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70#pic_center)
在这三个之中，都可以安装。为了确保兼容性，我推荐大家安装我在图片中软件包的后边打钩的两个软件包，其他可选。
>Tips：若你的设备内存不大只能容纳一个，且你要运行1.17以上的服务端，请安装openJDK-16-jre
>如果你要运行1.16.5及以下版本服务端，请安装openJDK-8-jdk

安装结束后，继续下一步。

#### 3.寻找Java路径
如果各位会使用Newterm以及SSH，可以自行安装Filza进行操作，如果不会，也没有关系，打开你的电脑吧。
首先在电脑上安装[FinalShell](http://www.hostbuf.com/)，打开FinalShell。
![Finalshell主页](https://img-blog.csdnimg.cn/fbb6d315fd9b481c8f940ac71f9f91f7.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
然后点击右上角的“小文件夹”
![在这里插入图片描述](https://img-blog.csdnimg.cn/4dfa5b8329284b0d9b1f048885643492.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
在弹出的连接管理器中，选择如图选项：
![添加设备](https://img-blog.csdnimg.cn/12d429ea3f804ac7ac6d6871902e24f1.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
在弹出的菜单中，选择SSH连接(Linux)

程序载入以下窗口：
![新建连接](https://img-blog.csdnimg.cn/35887e18fd0e444099a0bf1d53917e02.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
在名称中，输入你喜欢的任意名字
在主机中，填写你的设备在内网中的ip地址。（什么？你不知道？[看看别人的文章吧](https://jingyan.baidu.com/article/e5c39bf51fec0339d760339b.html)）
在认证分组框中，
用户名填写“root”
密码处填写“alpine”(如果你没有更改SSH默认密码的话)
比如这样：
![在这里插入图片描述](https://img-blog.csdnimg.cn/9d3df89c24fd4e93b81973489e8c1494.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)

然后选择确定。
你在连接管理器中，便看到了你的设备。
![](https://img-blog.csdnimg.cn/40ccedfb9987484aa1d92e6d12821a9b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
**接下来，十分关键的一步——找到Java的位置。**

---
双击你刚刚在连接管理器添加的设备，使得你的电脑于与手机建立连接。
![在这里插入图片描述](https://img-blog.csdnimg.cn/b678435a783d4e04bf29acc29a1c5bbb.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
不出意外的话，你会看到上面这样子的界面。
接下来，你需要用到最下面的文件管理。
![文件管理](https://img-blog.csdnimg.cn/45cebab5eb5340f185b4c5b85a7a0f73.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)

---

首先在文件管理中，
回到根目录 /
然后在右边的导航栏中，找到usr目录
![在这里插入图片描述](https://img-blog.csdnimg.cn/5b2f56c66ee640f790912f179bd38040.png)
然后按着一样的方法进入目录usr中的目录lib/jvm
![在这里插入图片描述](https://img-blog.csdnimg.cn/5ee1ebcc22474df5bc7694fc5c8a72c9.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
你便会看到你刚刚装的jdk版本文件夹。

选择一个版本的jdk，进入目录，在上方的文件目录栏中复制目录地址。
![在这里插入图片描述](https://img-blog.csdnimg.cn/38b4ab101a224c2986276c12bf70230f.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)

#### 4*.配置环境变量(可选)
插件在安装后不会自行配置环境变量，所以需要自行配置。

>当然你可以后续在sh文件中直接用JAVA路径来启动,但是你可能得先跟着安装下vim

这里引用mojang的话
![（doge）](https://img-blog.csdnimg.cn/089558fc5ae745c98eea5d7b08e69606.png)


>⚠注意！这里涉及系统底层的配置！请仔细阅读！否则可能影响手机的正常使用！本文作者不会对您操作造成的手机损坏负任何责任！

首先，在终端窗口中输入指令

```bash
apt-get install vim
```
等待vim安装。
然后再输入指令

```bash
vim /etc/profile
```
会进入iPhone的环境变量配置。
![vim](https://img-blog.csdnimg.cn/696e676d66c04fa8864610e0762bb03b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
按下键盘中的i键或者是insert键，
在文件末尾，加入两行变量：

```bash
export JAVA_HOME=/usr/lib/jvm/java-16-openjdk
export PATH=$JAVA_HOME/bin:$PATH
```
***注：在第一行中的“/usr/lib/jvm/java-16-openjdk”要替换成你在第三步末尾复制的文件地址
另外，在finalshell中是Ctrl+Shift+V粘贴！***
![要说的都在图里](https://img-blog.csdnimg.cn/84620537ccb04a6d88e27c27d47b734a.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
确保无误后，按下键盘的esc键，然后在英文状态下直接键入`:wq`
回到终端就代表保存成功。
然后输入`logout`注销终端。
![注销](https://img-blog.csdnimg.cn/68b1453dc7754fa78d221036d468d8cd.png)
然后按下enter键重新连接，
随后在终端中输入

```bash
java -version
```
![正常回显](https://img-blog.csdnimg.cn/98484e8f41354fba995dfa31515c37b0.png)
如果像上面那样，那么你可以进入下一步了。

如果还是报错，比如这样：
![报错](https://img-blog.csdnimg.cn/622d321ef7084a878636945587053dee.png)
检查一下你的步骤配置，有问题私聊留言。

>注：在重启失去越狱环境后，环境变量会失效，需要按照步骤重新配置。
>顺带一提，这玩意局限性挺高的，必须要在越狱环境下才能开服。但是一般人也不会拿日常使用的机子开服吧（



## 二、编写启动脚本

首先，在终端中输入

```bash
cd /
```
在下方的文件管理定位到根目录 /
然后再空白处右键，选择新建-文件夹
在输入窗口中输入用于存放的文件夹名称
![键入](https://img-blog.csdnimg.cn/4db1b39e96914be1b5debb15d45b161e.png)
此处以mcserver为例
![](https://img-blog.csdnimg.cn/d1ee939df83e4e8a88398dab2c018fdb.png)
创建后，输入`cd /`回到根目录（可能你本身已经在根目录了）

然后终端输入指令创建脚本

```bash
vim startmcserver.sh
```
在脚本中输入脚本（听着怪怪的？）

```bash
cd /mcserver
echo 正在启动Minecraft:Java服务器.....请稍等
java -jar /mcserver/server.jar
echo 服务器已退出！
```

>注：第一三行行的“/mcserver”是你刚才新建的文件夹名，“/server.jar”是你在下面那一步放置的服务端文件，等下会讲。

**如果你没有执行一、4*步骤配置环境变量，请使用下面的脚本:**

```bash
cd /mcserver
echo 正在启动Minecraft:Java服务器.....请稍等
/usr/lib/jvm/java-16-openjdk/bin/java -jar /mcserver/server.jar
echo 服务器已退出！
```

然后按下esc输入`:wq`退出。

如果你坚持到了这一步，恭喜！你很快就能启动服务器了！

## 三、准备必要文件
首先前往[Minecraft官网下载服务端](https://www.minecraft.net/zh-hans/download/server)
将下载下来的服务端改名为`server.jar`,通过文件管理的上传按钮放入你在之前建立的文件夹中
![在这里插入图片描述](https://img-blog.csdnimg.cn/cbe17d1533af4a368bbb3bf61a8c8470.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/61cf75fa40804c3883ba57deb3a85214.png)
## 四、启动服务端

回到根目录，在终端中输入

```bash
sh startmcserver.sh
```
你可能会看到这样子类似的报错，忽略它。
![在这里插入图片描述](https://img-blog.csdnimg.cn/65d477f6594442df803395fe0dcb2fd9.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
因为我们已经成功生成了eula.txt!
![在这里插入图片描述](https://img-blog.csdnimg.cn/4a75eb0b92534b48ae9418fc79f27a9d.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
然后双击打开eula.txt,把`eula=false`改成`eula=TRUE`
![在这里插入图片描述](https://img-blog.csdnimg.cn/6a95fd4c2064420ab3692c539669c3ea.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjcxODE5NA==,size_16,color_FFFFFF,t_70)
保存后重新执行

```bash
sh startmcserver.sh
```
等待一会，你就发现，服务器已经成功开始运行!!!
邀请你的小伙伴体验下吧！~~（尽管很卡）~~
 
---
⚠警告！在服务器运行时**不可关闭终端**！在服务器运行时**不可关闭终端**！在服务器运行时**不可关闭终端**！！！！！如果觉得麻烦可以参考补充信息。
## 写在最后
现如今，Minecraft玩家越来越多。人们想要开设一个服务器也是十分轻松。可~~哪个碳基生物~~ 谁又能想到手机上甚至是iPhone上也能运行Minecraft服务端呢？

有人会问，我有电脑不用电脑开，用iPhone开，我有时间多玩点游戏不好吗？
这你就不知道了，这就是折♂腾的乐趣（（（

哦对了，闪退或者强行关闭服务器会导致服务器回档，十分危险！
在关闭终端前请先输入`stop`来关服再关闭终端。
---

本文原创，发表于CSDN、bilibili，版权归本人所有，转载注明出处。
作者本人BLOG地址[blog.nuozhen.top](https://blog.nuozhen.top)
~~（小声bb两句，这不会是全网首发吧）~~ 