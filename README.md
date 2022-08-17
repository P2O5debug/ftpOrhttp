# FTP HTTP 局域网
****
## 弹弹play 的远程访问
> _借助 [**弹弹play**](https://www.dandanplay.com/)可以实现从手机端访问pc端的视频文件。_
<details>
<summary><strong><code>[点击展开] - PC端示例</code></strong></summary>

****
<img src="\photo\弹弹play服务启动.png">
</details>

****
<details>
<summary><strong><code>[点击展开] - 手机端示例</code></strong></summary>

****
<img src="\photo\弹弹play浏览器访问.png">

****
<img src="\photo\弹弹play客户端访问.jpg">

****
</details>

****
> _这里容易出现几个小问题_
-  _**PC** 端看似给出了三个内网 **ip** ，实际上不一定都能用，后面介绍 **FTP**时也会出现这种问题._
- _**PC**与手机必须在同一个局域网内，也就是连接同一个 **WIFI** ，与 **WIFI** 能否上网无关。_
- 用浏览器访问时需要输入的格式为 **ip 地址:端口** 例如：**192.168.0.8:80**
- _访问的是**弹弹play**媒体库的文件，可以添加文件。_

---

## 局域网访问
> _为了方便，将若干个连接同一 **WIFI**的设备组成的网络叫做局域网。_

_由**弹弹play**的例子可以看出，要实现局域网中的设备互联，需要一个实现共享功能的**服务端**，一个实现接受功能的**客户端**。_

- **PC**：**弹弹play** 服务端
- **手机**：**浏览器** 或者 **弹弹play** 客户端

_显然能够实现局域网共享的服务端与客户端不只一种。_

---

### **PC** 作为服务端
#### IIS管理器服务端操作
> **IIS管理器**作为服务端
<details>
<summary><strong><code>[1] - 搜索并打开 iis管理器</code></strong></summary>

****
<img src="\photo\iis管理器搜索界面.png">

****
</details>

<details>
<summary><strong><code>[2] - 在网站中添加 FTP站点，并设置名称和路径</code></strong></summary>

****
<img src="\photo\添加ftp站点1.png">

****
</details>

<details>
<summary><strong><code>[3] - 选择 ip地址和端口，SSL设置无，这里 ip不一定都能用</code></strong></summary>

****
<img src="\photo\添加ftp站点2.png">

****
</details>
<details>
<summary><strong><code>[4] - 权限放开，完成即可</code></strong></summary>

****
<img src="\photo\添加ftp站点3.png">

****
</details>

---
#### 客户端操作
> **手机管理器**作为客户端

_理论上浏览器也可以作为服务端，但操作后发现不行。_
_有些手机管理器并没有FTP功能，这里选用 **MT管理器**和 **mix管理器** 做演示_
<details>
<summary><strong><code>[1] - 打开文件管理器的 FTP添加功能，输入 ip地址和端口就行，账号密码服务端未设定</code></strong></summary>

****
<img src="\photo\mix管理器.png">

****
<img src="\photo\mt管理器.png">

****
</details>
<details>
<summary><strong><code>[2] - 打开新添加的 ftp盘就可以愉快地使用了。相当于usb连接，传输速度和路由器等网络环境有关</code></strong></summary>

****
<img src="\photo\mixftp.png">

****
<img src="\photo\mtftp.png">

****
</details>

---
> **IIS管理器作为服务端是最为麻烦的一种情况，会出现各式各样的问题。**

- _找不到 **IIS管理器**_
<details>
<summary><strong><code>[1] - 搜索“启用或关闭 Windows功能”</code></strong></summary>

****
<img src="\photo\程序和功能.png">

****
</details>
<details>
<summary><strong><code>[2] - 在 “Internet Information Services”中开启FTP服务器</code></strong></summary>

****
<img src="\photo\iis开启.png">

****
</details>
</br>

- _连接不上，**防火墙**未开启_
<details>
<summary><strong><code>[1] - 搜索并打开“防火墙和网络保护” </code></strong></summary>

****
<img src="\photo\防火墙.png">

****
</details>
<details>
<summary><strong><code>[2] - 在“允许应用通过防火墙”中开启 FTP服务器</code></strong></summary>

****
<img src="\photo\防火墙2.png">

****
</details>
<details>
<summary><strong><code>[3] - 搜索并打开防火墙</code></strong></summary>

****
<img src="\photo\防火墙3.png">

****
</details>
<details>
<summary><strong><code>[4] - 在“入站规则”中新建一个端口规则</code></strong></summary>

****
<img src="\photo\防火墙4.png">

****
</details>
<details>
<summary><strong><code>[5] - 添加需要通过的端口，例如“21,80”······</code></strong></summary>

****
<img src="\photo\防火墙5.png">

****
</details>
</br>

- 连接不上，**文件夹权限问题**
<details>
<summary><strong><code>[1] - 我这里容易在C盘共享出现问题，D盘正常，将C盘的权限改为和D盘一样</code></strong></summary>

****
<img src="\photo\文件夹权限.png">

****
</details>
<details>
<summary><strong><code>[2] - 或者新建一个本地用户，然后添加进文件夹的权限中</code></strong></summary>

****

> 管理员方式启动cmd

```
net 用户名 用户密码 /add       //添加本地用户

net 用户名 /delete            //删除本地用户
```
<img src="\photo\cmd.png">
<br/>

> 添加进文件夹的权限中

<img src="\photo\文件夹权限.png">

****
</details>

---

#### everything作为服务端操作

 _[**everything**](https://www.voidtools.com/zh-cn/downloads/)用起来十分简单，准确来讲，是IIS管理器不好用。_

- 操作前先记录下 **ip地址**
<details>
<summary><strong><code>[1] - 看代码</code></strong></summary>

****

> 搜索 **cmd**并打开，输入
```
ipconfig
```

> 找到“无线局域网”中的“IPv4地址”记录下来

****
</details>
<details>
<summary><strong><code>[2] - 或者看 WIFI</code></strong></summary>

****
WIFI属性中找到IPv4地址记录下来
****
</details>
<br/>

> **FTP操作**
<details>
<summary><strong><code>[1] - 打开 everything,选择“工具”中的“选项”，输入本机的 ip地址，选择任意一个端口，点右下角应用即可</code></strong></summary>

****

<img src="\photo\everything浏览器访问.jpg">

****
</details>

_此时服务端已经配置好了，不需要再弄什么防火墙或者权限，就可以用文件管理器中的 FTP服务访问。_

> **HTTP操作**
<details>
<summary><strong><code>[1] - 打开 everything,选择“工具”中的“选项”，输入本机的 ip地址，选择任意一个端口，点右下角应用即可，那个服务器页面什么的不会写就不用选了</code></strong></summary>

****
<img src="\photo\everything的http.png">

****
</details>

<details>
<summary><strong><code>此时服务端已经配置好了，在浏览器中输入网址即可访问</code></strong></summary>

****

> 输入时注意是 **http**，不要忘记端口
```
http://192.168.0.8:80
```
<img src="\photo\everything浏览器访问.jpg">

****
</details>

---

> **FTP**与 **HTTP**在实际体验上的区别是一个可以上传，而另一个不能。

---

#### python建立http
建立后可用手机访问
<details>
<summary><strong><code>[1] - 下载 python并确定已添加进环境变量</code></strong></summary>

****
[点此转到python](https://www.python.org/)

****
</details>

<details>
<summary><strong><code>[2] - 在“资源管理器”中找到要分享的文件夹，并用 cmd打开</code></strong></summary>

****

> 在地址栏键入
```
cmd
```

> 输入代码
```
python -m http.server 3000    //3000是端口
```
> 按下 **ctrl+c**停止代码运行

****
</details>
<details>
<summary><strong><code>[3] - 在手机浏览器中访问</code></strong></summary>

****

>浏览器地址输入
```
http://192.198.0.5:3000
```
<img src="\photo\pythonhttp.jpg">

****
</details>

## 将手机作为服务端

### 文件管理器作为服务端
> 手机开启 **FTP服务**很简单，只要在文件管理中找到一个叫“远程管理”的功能。
手机自带的管理器没有，找一个有此功能的就行。

<details>
<summary><strong><code>[1] - 手机开启“远程管理”</code></strong></summary>

****
<img src="\photo\手机远程管理.png">

****
</details>
<details>
<summary><strong><code>[2] - 在“资源管理器”中键入 FTP地址</code></strong></summary>

****
<img src="\photo\pc远程管理.png">

****
</details>

---

- 以上操作均在局域网中进行
- 以上所指 **ip 地址**均为**内网 ip**
- 非相关专业人士