# -Great Wall-

>随着时代的进步，互联网普及到千家万户，然而中国大陆的互联网开始走向封闭，一堵互联网的墙，如长城一般竖立在国内网络与国际网络之间。这堵墙，民间称之为防火长城（英语：Great Firewall，下简称：GFW），GFW封锁了例如Google,Twitter,Facebook等外网平台，中国大陆的居民只能使用国内或国外未被封锁的的网站[关于GFW,可前往维基百科(翻墙需要)查阅](https://zh.wikipedia.org/wiki/%E9%98%B2%E7%81%AB%E9%95%BF%E5%9F%8E)。大陆网民只能通过“翻墙”这一手段来访问被封禁的网站。而由于信息封锁的原因，不少人无从得知翻墙的方法。因此，我决定开始进行完整的翻墙教学编写。

---

## 注意事项

根据《中华人民共和国计算机信息网络国际联网管理暂行规定》，“计算机信息网络直接进行国际联网，必须使用邮电部国家公用电信网提供的国际出入口信道。任何单位和个人不得自行建立或者使用其他信道进行国际联网。”如违反上述规定，公安机关会责令停止联网，给予警告，可以并处15000元以下的罚款；有违法所得的，没收违法所得。

尽管如此，您如果按照我们的方法，并且不在外网发布或（在行为上表示）赞同黄赌毒反动等言论，您是不违法的。

>其实这条法规规定的是物理信道，而非下面讲的代理。不过当地叔叔要抓你你也没办法。

**千万不要在大陆翻墙发布/赞同 反动/色情等言论！否则谁都保不了你。**

## 准备工作

你需要:

一台需要翻墙的设备

翻墙软件(等下会讲)

机场(等下会讲)

一双手

内有足量钱的钱包

一个IQ!=0的脑瓜子


### 翻墙软件

>市面上有不少翻墙软件，实现原理不尽相同。这里分设备种类推荐几款翻墙软件，有的需要付费，请酌情选择。

#### Android

首先是V2RayNG,完全免费,开源,使用的核心是XRay和v2fly。

开源链接:https://github.com/2dust/v2rayNG

软件Release下载链接:https://github.com/2dust/v2rayNG/releases

Github直接下载1.7.35 Pre-release:https://github.com/2dust/v2rayNG/releases/download/1.7.35/v2rayNG_1.7.35.apk

国内服务器上海快速下载1.7.35 Pre-release:https://drive-america.nuozhen.top/v2rayNG_1.7.35.apk

国内备用服务器下载1.7.35 Pre-release:https://drive.nuozhen.top:3232/Softwares/v2rayNG_1.7.35.apk

---

另外一个是Clash For Android

一样免费开源，使用的核心是Clash。

开源链接:https://github.com/Kr328/ClashForAndroid

软件Release下载链接:https://github.com/Kr328/ClashForAndroid/releases

Github直接下载2.5.12:https://github.com/Kr328/ClashForAndroid/releases/download/v2.5.12/cfa-2.5.12-premium-universal-release.apk

国内服务器上海快速下载2.5.12:https://nuozhen.oss-cn-shanghai.aliyuncs.com/cfa-2.5.12-premium-universal-release.apk

国内备用服务器下载2.5.12:https://drive.nuozhen.top:3232/Softwares/cfa-2.5.12-premium-universal-release.apk


#### iOS

iOS目前就只有Shadowrocket可用，并且需要切换外区**购买**。

首先你需要一个外区账号，然后在App Store搜索Shadowrocket购买即可。

#### Windows

V2RayN - A V2Ray client for Windows, support Xray core and v2fly core.

V2RayN开源免费，支持Xray和v2fly内核。

>目前最新最热的6.7 Pre-release使用了.NET 6 需要先下载安装[Microsoft .NET 6.0 Desktop Runtime](https://download.visualstudio.microsoft.com/download/pr/ba2ece7b-686a-4bda-b7d7-8cc3b8964d66/8eee13e44d90345d40c1b262c78aad6a/windowsdesktop-runtime-6.0.12-win-x64.exe)

开源链接:https://github.com/2dust/v2rayN

软件Release下载链接:https://github.com/2dust/v2rayN/releases/

Github直接下载6.7 Pre-release:https://github.com/2dust/v2rayNG/releases/download/1.7.35/v2rayNG_1.7.35.apk

国内服务器上海快速下载6.7 Pre-release:https://nuozhen.oss-cn-shanghai.aliyuncs.com/v2rayN-With-Core.zip

国内备用服务器下载6.7 Pre-release:https://drive.nuozhen.top:3232/Softwares/v2rayN-With-Core.zip

---

Clash For Windows，这是一个免费的Clash GUI软件，不过虽然它"For Windows"，但是它同时支持Windows、Linux和macOS。

软件下载:https://github.com/Fndroid/clash_for_windows_pkg/releases

Github直接下载v0.20.15:https://github.com/Fndroid/clash_for_windows_pkg/releases/download/0.20.15/Clash.for.Windows-0.20.15-win.7z

国内服务器上海快速下载v0.20.15:https://nuozhen.oss-cn-shanghai.aliyuncs.com/Clash.for.Windows.Setup.0.20.15.exe

#### MacOS

可以用上一节讲的Clash For Windows

国内服务器上海快速下载v0.20.15:https://nuozhen.oss-cn-shanghai.aliyuncs.com/Clash.for.Windows-0.20.15.dmg

#### Linux

同上

国内服务器上海快速下载v0.20.15:https://nuozhen.oss-cn-shanghai.aliyuncs.com/Clash.for.Windows-0.20.15-x64-linux.tar.gz

### 关于机场

#### 什么是机场

要了解什么是机场，就要先了解什么是Shadowsocks。

>Shadowsocks（简称SS）是一种基于Socks5代理方式的加密传输协议，也可以指实现这个协议的各种开发包。目前包使用Python、C、C++、C#、Go语言、Rust等编程语言开发，大部分主要实现（iOS平台的除外）采用Apache许可证、GPL、MIT许可证等多种自由软件许可协议开放源代码。Shadowsocks分为服务器端和客户端，在使用之前，需要先将服务器端程序部署到服务器上面，然后通过客户端连接并创建本地代理。

>为了避免关键词过滤，网民会根据谐音将ShadowsocksR称为“酸酸乳”（SSR），将Shadowsocks称为“酸酸”（SS）。另外，因为Shadowsocks(R)的图标均为纸飞机，所以专门提供Shadowsocks(R)或类似服务（如V2Ray和TROJAN）的网站则就被称为了“机场”。

因此，机场则是提供节点服务的网站。一般机场在你购买套餐后会给予你一个"订阅链接"，将链接导入到代理软件，更新订阅即可使用机场套餐内的节点。

>注意，订阅链接不可泄漏，否则可能会导致预期外的大量流量使用。

这是几个机场推荐，可以参考看看。

https://github.com/hwanz/SS-SSR-V2ray

我用的是这个:https://ssrelay.cc/#/register?code=wF3fH5OX

**一些意味**：部分谋求长时稳定发展的机场正进一步私有化群组，不再对外界公开服务细节，包括但不限于真实用户的使用反馈/讨论等等；另，为应对不断增加的不可抗力事件（事件中有真的也有假的），如运营商(联通/电信/移动) 在政策压力下直接下场拔线，年付务必谨慎，如无必要，月付/季付/半年付（最多）即可（部分机场月付很贵，咬咬牙还是会犹豫良久，而年付相对实惠很多，没有威逼，但有**足够的利诱**）。

**关于跑路**：Rixcloud/喵帕斯/Blinkload/速蛙云/世外桃源等等一系列已经跑路的机场告诉我们，机场的尽头就是跑路。改头换面重复收割韭菜的也有。

**关于备用**：每年的关键时间节点，都会听到哀嚎一片。原因包括但不限于机场上游拔线（有主动的/有被动的），受拔线影响机场近期可能会因找不到合适的上游（~~不愿接收或增配IDC资源~~）导致不稳定状况增加或持续；），排除其节后预谋跑路的成分，建议暂时备好备用机场(月付即可)，用于这段时间进行过度；

**特别提醒**：尽量月付，渐进式季付、半年付；

## 写在最后

**一些实用性建议**：

1. 使用非大陆邮箱进行注册机场（使用Gmail/Outlook/Yahoo邮箱等）；
2. 切记以上邮箱不要跟任何国内业务进行绑定（微信/QQ/支付宝/国行App相关注册业务等）；
3. 墙外非法外，谨言慎行；
4. 关于机场是否有你的上网浏览记录？有且可以实时查看；（包括但不限于你的IP/什么时间访问了什么网站等等）
5. 遵循1、2、3点，你的浏览记录不会有太多实用价值，可以说是毫无用处（你爱刷Twitter? Youtube? or P*rnhub? 大丈夫! 但，这里建议大家，不如多看看，多学习一些较为有用的东西；不要把时间浪费在奶头乐上面；整天沉溺游戏、美女、P*rn...，不自知，不自学，甚至一年都不读一本书... 试想想谁会愿意关注这些废物呢？纯属浪费时间。）
   
墙外很多东西你在内网很少很难见到的，有些东西误导人的成分很大，所以你自己要有点思辨能力，不要人云亦云。翻墙同时也是一个锻炼独立思考能力不错的一个方式，但是请注意，在你学会辨别信息真假对错之前，不要下定论，不要参与讨论。

>你所看到的，只是他们想让你看到的。

**完**