## 该文档是我在使用Ubuntu虚拟机配置Clash时的一些记录

### 硬件平台

- PC平台：Windows 11
- 虚拟机平台：VMWare Workstation Pro
- Linux发行版：Ubuntu-22.04.1
- Clash版本：Clash for Windows 0.20.4

### 适合人群

适合对Windows配置网络代理有所了解且第一次在Ubuntu配置Clash的**新手**。

### 为什么要配置Clash

虚拟机不与主体机共享网络？（~~没有学过网络相关的知识，所以不太了解其中的详细原理~~）但是显然在Ubuntu Network设置中有设置网络代理（Network Proxy）这一选项，也就意味着：

- 当我们在虚拟机中使用网络时，如果仅仅使用大陆允许的网络链接，自然可以把Network Proxy中的选项改为Automatic。

- 但是当我们需要访问一些诸如[Github](https://github.com)，[youtube](https://youtube.com)等等网站需要解决开发中的问题的时候，上述方法就不可行了，在Windows上我们自然可以选择使用网络代理平台[Clash](https://github.com/Fndroid/clash_for_windows_pkg/releases)，通过订阅链接进行下载，类似这样：
  
  ![Clash For Windows](https://github.com/Melmaphother/Ubuntu-Clash/blob/master/pic/windows%E9%85%8D%E7%BD%AEclash.png)
  
   不过Clash在Ubuntu平台上的GUI版本貌似不太好用？不如使用命令行进行配置，我本人配置时参考了诸多文章，如[知乎专栏](https://zhuanlan.zhihu.com/p/598337110)，[Ubuntu系统代理设置/JMS/Clash - 简书](https://www.jianshu.com/p/cc3a95e6f3a4)，[Ubuntu 配置为旁路由实现透明代理（Clash） - 掘金](https://juejin.cn/post/7065548789997633567)，但是它们所说的功能有的有些过于繁杂，不太适合新手，最重要的是：它们忽略了一点，就是大部分文章的受众是第一次在Ubuntu中配置Clash的，我们在Ubuntu中是不能访问某些网站的，也就不能直接在Ubuntu命令行中做它们所述的操作，如`wget`等（~~因为连不上某些链接~~）。
  
  那么，如果你是一名新手，可以参考我下面的配置记录。

### 配置记录

1. 在Windows平台下载Clash的Linux版本[Clash for Linux](https://github.com/Dreamacro/clash/releases)，选择`clash-linux-amd64-vx-vx.xx.x.gz`

2. 打开Ubuntu的文件夹，选择Downloads文件夹，将刚刚下载的压缩包Copy进该文件夹内，注意不要直接拖文件，尽量在Windows的资源管理器中复制然后paste进Ubuntu的文件中

3. 打开Terminal，cd到Downloads文件下：
   
   ```tex
   cd Downloads
   ```

4. 解压该压缩包
   
   ```tex
   gunzip clash-linux-amd64-vx-vx.xx.x.gz
   ```

5. 此时你的Downloads中只有解压后的文件了，现在重命名它否则太长了不好操作
   
   ```tex
   mv clash-linux-amd64-vx-vx.xx.x.gz clash
   ```

6. 现在你的Downloads中应该只有clash这一个东西了，此时我们建一个文件夹将它放进去，让他与之后的配置文件处在同一个目录下防止文件过多冗杂：
   
   ```tex
   mkdir Clash //(大写C为了与clash辨别)
   mv clash ./Clash
   ```

7. 此时我们已经安装好了clash，现在需要将你的订阅链接下载到clash中，**然鹅**，我们发现现在我们根本用了全局代理，所以我们甚至不能连接到订阅链接的提供方网站。也就是说：此时使用：
   
   ```tex
   wget -O config.yaml [订阅链接]
   ```
   
   是根本没有用的，提示半天`error connect`，那么我们可以直接在Windows中得到config.yaml然后Copy进Ubuntu中，我们只需要将你的订阅链接复制到浏览器输入栏，此时会直接跳出下载选项，**一定一定**要把这个文件重命名为
   
   ```tex
   config.yaml
   ```
   
   下载完后还是跟`2.`中的操作一样，将其复制粘贴至你的Clash文件夹中。
   
   此时你的Clash文件夹中应该包括两个文件
   
   ```tex
   - clash
   - config.yaml
   ```

8. 下载[Country.mmdb](https%3A//github.com/Loyalsoldier/geoip/releases/download/202212010123/Country.mmdb)，一个道理，还是在Windows平台上先下载，然后复制粘贴至你的Clash文件夹中。
   
   此时你的Clash文件夹中应该包括三个文件
   
   ```tex
   - clash
   - config.yaml
   - Country.mmdb
   ```

9. 剩下的事情就很简单了，首先进入Clash文件夹：
   
   ```tex
   cd Clash
   ```
   
   设置clash文件的权限：
   
   ```tex
   chmod +x clash
   ```
   
   设置网络代理
   
   打开设置，点开第一个Network，再点开Network proxy，配置如下：
   
   ![](https://github.com/Melmaphother/Ubuntu-Clash/blob/master/pic/%E8%AE%BE%E7%BD%AE%E7%BD%91%E7%BB%9C%E4%BB%A3%E7%90%86.png)
   
   启动clash：
   
   ```tex
   ./clash -d .  (不要忘了这个点！！)
   ```

### 效果

![](https://github.com/Melmaphother/Ubuntu-Clash/blob/master/pic/%E6%95%88%E6%9E%9C%E5%9B%BE.png)

之后我们就可以自由使用几乎所有网络链接了。