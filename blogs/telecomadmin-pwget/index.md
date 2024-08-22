# 获取天翼宽带家庭网关 (电信光猫) 管理员telecomadmin密码

## 设备信息

相关设备的信息如下: 

10G-EPON 天翼网关(无Wi-Fi)

- 设备型号: TEWA-1100E

- 生产日期: 2022-05-03

- 地区: 福建厦门

## 准备环境

在获得密码之前，你的电脑必须具有任意Telnet客户端。

这里推荐使用Windows自带的Telnet命令行工具。安装方法如下: 

1. 打开Windows上的 `控制面板`

2. 单击 `程序` - `启用或关闭 Windows 功能`

3. 下滑，并勾选 `Telnet 客户端`

4. 如提示需要安装相关依赖组件包，请安装。

5. 点击 <button>确定</button> 按钮

6. 等待Windows完成安装。

7. 打开命令提示符，输入`telnet`，按下<button>Enter</button>，你应该能成功进入Telnet命令行。

> 更多信息可以自行搜索。

## 实操

### 1. 连接上网关

使用网线将你的电脑与网关的任意LAN口连接。

### 2. 访问网关后台

天翼网关有两个后台网页，一个是面向普通用户的，另一个是面向装维师傅的。

直接访问网关的IP (一般是192.168.1.1) 默认的是`80`端口的管理后台，提供的功能较为基本。因此我们需要访问装维管理后台。装维后台的端口为`8080`。因此我们访问 http://192.168.1.1:8080/login.html 访问管理后台。

### 3. 登录网关

使用用户管理账号 (useradmin) 登录管理后台(默认的账户密码在光猫底部标签)。

登录后你应该能看见大多数光猫运行参数，但不能修改大部分参数。

### 4. 获取sessionKey

在管理后台，点击`管理`选项卡，再点击`设备管理`子栏目。在<button>恢复出厂设置</button>按钮上按下右键，点击检查。

你应该能看到眼前的开发人员工具被定位到了一行`input`元素:

```html
<input type="button" value=" 恢复出厂设置 " onclick="restoreClick()">
```

该元素是一个按钮，按下后执行在JavaScript中被定义的 `restoreClick()` 函数。

接下来我们需要找到 `restoreClick()` 函数的实际实现。我们向上翻元素代码，可以看到`<head>` 元素内有一个`<script>`元素:
```html
<script type="text/javascript">
    <!--

    //恢复出厂设置
    function restoreClick() {
        var loc = 'restoreinfo.cgi?';

        loc += 'set3_sessionKey=' + '1744022389638093331';
        var code = 'location="' + loc + '"';

        if (confirm("确认恢复出厂设置?"))
            eval(code);
    }

    //重启
    function btnReset() {
        var loc = 'rebootinfo.cgi?';

        loc += 'set4_sessionKey=' + '6756266349440544';

        var code = 'location="' + loc + '"';
        eval(code);

    }

    //页面初始化
    function frmLoad() {
        with ( document.forms[0] ) {

        }
    }
    //-->
</script>
```

可以看到两个sessionKey，`set3_sessionKey` 和 `set4_sessionKey`。两个sessionKey分别用于恢复出厂设置和重启的参数拼接。我们保留 `set3_sessionKey` 的值备用。

> 实测这俩sessionKey是会动态变化的，因此应在网关后台自动退出前尽快完成下面步骤。

### 5. 使能Telnet

在浏览器中，输入以下网址:

```
http://192.168.1.1:8080/telandftpcfg.cmd?action=add&telusername=admin&telpwd=admin&telport=23&telenable=1&ftpusername=useradmin&ftppwd=ftpadmin&ftpport=21&ftpenable=1&set3_sessionKey=<set3_sessionKey>
```

然后将链接最后的`<set3_sessionKey>`替换为你在[第4步](#4-获取sessionkey)获取的 
`set3_sessionKey` 值。例如我上一步获得的 `set3_sessionKey` 值为 `1744022389638093331` ，我就应该将链接替换为: 

```
http://192.168.1.1:8080/telandftpcfg.cmd?action=add&telusername=admin&telpwd=admin&telport=23&telenable=1&ftpusername=useradmin&ftppwd=ftpadmin&ftpport=21&ftpenable=1&set3_sessionKey=1744022389638093331
```

按下<button>Enter</button> 访问该网址。你应该能看到已经设定好的Telnet和FTP参数。

### 6. (可选) 修改Telnet和FTP参数

观察[上一步](#5-使能Telnet) 的设置链接，你应该能发现它做了什么:

```
http://192.168.1.1:8080/telandftpcfg.cmd? //控制和设置Telnet & FTP的url

action=add
&telusername=admin //设置Telnet 用户名 (可修改)
&telpwd=admin //设置Telnet 密码
&telport=23 //设置Telnet 端口
&telenable=1 //使能Telnet (bool值，0为关闭Telnet，1为启用Telnet)

&ftpusername=useradmin // 设置FTP 用户名
&ftppwd=ftpadmin // 设置FTP 密码
&ftpport=21 //设置FTP 端口
&ftpenable=1 //使能FTP (bool值，0为关闭FTP，1为启用FTP)

&set3_sessionKey=<set3_sessionKey> //指定鉴权所使用的sessionKey
```

修改url参数并重新拼接访问，即可修改页面上展示的Telnet和FTP设置。

> 页面上的参数改了没用哦 ~

> 每次设置过后都必须刷新管理后台并重新获取一次sessionKey。

### 7. 使用Telnet连接网关

打开命令提示符 (CMD) 或Powershell，输入 `telnet` 进入Telnet命令行。

输入`?`并按下回车可以查看Telnet客户端命令行帮助。

在Telnet命令行中，我们输入指令连接网关:

```cmd
open 192.168.1.1
```

如果你有更改Telnet端口(而非默认端口23)，输入
```cmd
open 192.168.1.1 <你修改的端口>
```

按下回车，Telnet客户端会要求你输入账户密码。

我们在`Login: `后面输入你设置的Telnet账户 (如果你没有在 [第六步](#6-可选-修改telnet和ftp参数) 修改Telnet账户，那它默认是 `admin`)，按下回车。

同样地，在`Password: `后面输入你设置的Telnet密码 (如果你没有在 [第六步](#6-可选-修改telnet和ftp参数) 修改Telnet账户，那它默认是 `admin`)，按下回车。

你应该已经成功连接并登录到网关。

### 8. 进入Super User账户

在Telnet命令行中，输入指令:

```bash
su
```

随后在`Password: ` 后输入su密码:

> 密码需要计算...请找论坛大神！

> 未完待续...
